# AWS VPC with Variable-Size Subnets

## Project: asymmetric-vpc-build

---

## 📘 Overview

This project builds a production-style AWS VPC architecture using Terraform, featuring variable-sized subnets that simulate real enterprise network requirements. The design includes:

* A `/16` VPC
* Six subnets of different sizes
* Internet Gateway
* **Single** NAT Gateway
* Dedicated route tables per subnet
* Strict public/private isolation
* Comprehensive tagging

---

## 🏗️ 1. VPC Configuration

### **VPC Name:** `asymmetric-vpc`

### **Specifications**

* **CIDR Block:** `10.0.0.0/16`
* **DNS Hostnames:** Enabled
* **DNS Resolution:** Enabled

<img width="1365" height="283" alt="1" src="https://github.com/user-attachments/assets/786739b9-e774-492e-8cea-acebb82a710e" />



<img width="1398" height="657" alt="2" src="https://github.com/user-attachments/assets/b33bdea7-a49d-4e8c-880f-30315a0989da" />

### **Tags (applied to all resources)**

```
Environment = "production"
Owner       = "network-team"
Project     = "asymmetric-vpc-build"
CostCenter  = "AWS-Networking"
```

---

## 🧩 2. Subnet Architecture


<img width="1388" height="477" alt="3" src="https://github.com/user-attachments/assets/4b353b4d-84e8-4d47-82dd-d054098bdff3" />


This VPC contains **six subnets**, each with a **unique CIDR size** to match expected IP usage.

| Subnet Name      | Required IPs | CIDR | Type    | Purpose                       |
| ---------------- | ------------ | ---- | ------- | ----------------------------- |
| Public Subnet A  | ~256         | /24  | Public  | Bastion, ALB, small services  |
| Public Subnet B  | ~4,096       | /20  | Public  | Medium-scale public workloads |
| Public Subnet C  | ~8,192       | /19  | Public  | Large ingress workloads       |
| Private Subnet A | ~1,024       | /22  | Private | App servers                   |
| Private Subnet B | ~512         | /23  | Private | Internal microservices        |
| Private Subnet C | ~8,192       | /19  | Private | Databases, internal clusters  |

### **Additional Requirements**

#### **Public Subnets**

* Spread across different AZs
* Auto-assign public IPs → Enabled
* Routed to Internet Gateway

#### **Private Subnets**

* Spread across multiple AZs
* Auto-assign public IPs → Disabled
* Outbound internet via **single NAT Gateway**

### **Subnet Tagging**

```
Tier = "public"  /  "private"
```

---

## 🌐 3. Internet Gateway

<img width="1197" height="181" alt="5" src="https://github.com/user-attachments/assets/823b3010-0928-4b58-819f-51a35ddba204" />


* **Name:** `asym-igw`
* Attached to the VPC
* Public route tables use IGW as default route

---

## 🔄 4. NAT Gateway Design

<img width="1382" height="210" alt="6" src="https://github.com/user-attachments/assets/cded7764-16a9-4c75-8191-5ab62d332024" />


### **Strategy:** Single NAT Gateway

A single NAT Gateway is deployed in the **largest public subnet** (`Public Subnet C – /19`).

### **Why?**

* Cost-efficient
* Simplifies routing
* Suitable for training & POC environments

### **NAT Gateway Details**

* Deployed in Public Subnet C
* Has a dedicated Elastic IP
* Default routes of all private subnets → NAT Gateway

### ⚠ Trade-offs

* **Single point of failure**
* **Cross-AZ charges** for private subnets in other AZs

---

## 🧭 5. Route Table Structure


<img width="1382" height="305" alt="4" src="https://github.com/user-attachments/assets/3b037476-97da-4ee9-a046-1c640e36127e" />


### **Public Route Tables**

* One route table per public subnet
* Default route: `0.0.0.0/0 → Internet Gateway`

### **Private Route Tables**

* One route table per private subnet
* Default route: `0.0.0.0/0 → NAT Gateway`

---

## 🔗 6. Subnet → Route Table Mapping

| Subnet    | Route Table Type | Default Route Target |
| --------- | ---------------- | -------------------- |
| Public A  | Public RT        | IGW                  |
| Public B  | Public RT        | IGW                  |
| Public C  | Public RT        | IGW                  |
| Private A | Private RT       | NAT Gateway          |
| Private B | Private RT       | NAT Gateway          |
| Private C | Private RT       | NAT Gateway          |

---

## 🏷️ 7. Tagging Standard

All resources include:

```
Environment = "production"
Owner       = "network-team"
Project     = "asymmetric-vpc-build"
CostCenter  = "AWS-Networking"
Tier        = "public" / "private"
```

This ensures:

* Cost tracking
* Ownership clarity
* Automation compatibility

---

## 🗺️ 8. High-Level Architecture Diagram

```
                              +------------------------+
                              |       Internet         |
                              +-----------+------------+
                                          |
                                      (IGW)
                                          |
    --------------------------------------------------------------------
    |                        VPC: 10.0.0.0/16                         |
    |                                                                  |
    |  Public A (/24)    Public B (/20)    Public C (/19)             |
    |      AZ-a              AZ-b              AZ-c                    |
    |                                          |                       |
    |                                   +--------------+               |
    |                                   | NAT Gateway  |               |
    |                                   | (EIP attached)|              |
    |                                   +-------+------+               |
    |                                           |                      |
    |------------------------------------------------------------------|
    | Private A (/22)  Private B (/23)   Private C (/19)              |
    |     AZ-a             AZ-b              AZ-c                     |
    |      |                 |                 |                      |
    |  Routes → NAT GW   Routes → NAT GW   Routes → NAT GW            |
    -------------------------------------------------------------------
```

---

## 📝 10. Project Justification

This architecture showcases:

* Asymmetric subnet sizing (realistic enterprise requirement)
* Strict isolation between public & private tiers
* Per-subnet routing for visibility & control
* Single NAT Gateway for cost-efficient environments
* Strong tagging to support governance and cost management

---

**End of Documentation**
