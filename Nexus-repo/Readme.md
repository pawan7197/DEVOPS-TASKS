# 🧩 Multi-Server Java Application Build, Store, and Deployment System

## 🎯 Objective
This project demonstrates a **multi-server CI/CD setup** for a Java Web Application.  
It uses three servers to handle the **build**, **artifact storage**, and **deployment** processes:

- 🏗️ **Build Server** – Builds the Java app using Maven  
- 📦 **Nexus Repository Server** – Stores the built `.war` artifact  
- 🚀 **Deploy Server** – Deploys the app to Apache Tomcat  

The Java Web Calculator App from GitHub is used as the source project:  
👉 [Java-Web-Calculator-App](https://github.com/mrtechreddy/Java-Web-Calculator-App.git)

---
## INSATNCES

<img width="1585" height="466" alt="Image" src="https://github.com/user-attachments/assets/44982e4f-f8df-4631-89c4-91520b520cdf" />

## 🖥️ Server Roles

### 1️⃣ Build Server
**Purpose:** Clone, build, and deploy artifacts to Nexus.

#### Steps:
**BUILD-SERVER-CONNECT**

<img width="611" height="215" alt="Image" src="https://github.com/user-attachments/assets/2ad1a608-4d12-4dc1-98a4-1b373abe4106" />

**GIT-CLONE**

<img width="868" height="288" alt="Image" src="https://github.com/user-attachments/assets/e2325719-ce70-4894-93f0-ba84a30f88e2" />

**JAVA-INSTALLATION**

<img width="765" height="63" alt="Image" src="https://github.com/user-attachments/assets/2b226609-f03a-4953-af4e-c49c744ddc7a" />

**MAVEN-INSTALLATION**

<img width="688" height="51" alt="Image" src="https://github.com/user-attachments/assets/2ee2d0fa-ff16-404c-82f3-fe14a020dfee" />

**MAVEN-VALIDATE-PACKAGE**

<img width="1563" height="509" alt="Image" src="https://github.com/user-attachments/assets/6a62fbd7-a582-4b24-b7dc-8d9b27541d74" />

**BUILD-SUCCESS**

<img width="1204" height="224" alt="Image" src="https://github.com/user-attachments/assets/9f650445-84eb-43c8-b870-4db5d20cd7c8" />



### NEXUS-SERVER :
Purpose: Store and manage build artifacts (.war files)

Steps:
**NEXUS-SERVER-CONNECT**

<img width="663" height="60" alt="Image" src="https://github.com/user-attachments/assets/92cf62e0-bedc-4be7-9eca-3cb4ef454a54" />

**NEXUS-DOWNLOAD**

<img width="1595" height="411" alt="Image" src="https://github.com/user-attachments/assets/4ad5e914-cc5a-4d5a-a46a-c36f1edd0a23" />




**EXTRACT-FILE**

<img width="1419" height="123" alt="Image" src="https://github.com/user-attachments/assets/5a0bdaf0-4bea-41be-920d-9bb54301f690" />


**NEXUS-START**

<img width="1361" height="377" alt="Image" src="https://github.com/user-attachments/assets/3203a7b2-fb7b-4bc6-8a14-dad07f172d65" />
```
cd nexus-3*
./bin/nexus start
```

**ACCESS-NEXUS**

<img width="1581" height="593" alt="Image" src="https://github.com/user-attachments/assets/9dfa6b52-8169-4cd8-8a8f-8edf97f263b5" />

```
Access Nexus UI:
http://<NEXUS_SERVER_IP>:8081
```

**NEXUS-LOGIN**

<img width="1561" height="813" alt="Image" src="https://github.com/user-attachments/assets/162dd886-6d3b-4384-bc31-64e22fd765e1" />

**GO TO-BROWSER**

<img width="1567" height="688" alt="Image" src="https://github.com/user-attachments/assets/11497073-6637-4b50-9d93-2034cd91109b" />

**CREATE-REPOSITORY**

<img width="623" height="266" alt="Image" src="https://github.com/user-attachments/assets/480c6d1e-15f9-44ca-a45c-6d7ecd35591b" />

**GO TO-HOSTED REPO**

<img width="1572" height="660" alt="Image" src="https://github.com/user-attachments/assets/c9e1d9ff-25db-4155-b757-349271dfda29" />

**REPO-CREATED**

<img width="1599" height="607" alt="Image" src="https://github.com/user-attachments/assets/c757b56c-7ba6-4e63-bd77-997be71466cd" />

**COPY-REPO LINK**

<img width="1557" height="538" alt="Image" src="https://github.com/user-attachments/assets/25524c2b-0707-4587-bbc1-3e39e5499f40" />

**UPDATE THE NEXUS ID AND COPY LINK IN POM.XML FILE**

<img width="940" height="845" alt="Image" src="https://github.com/user-attachments/assets/5f17b226-19d4-46f6-8d30-ff5857582da4" />

**IN BUILD SERVER-CHANGE THE SETTINGS IN SETTING.XML FILE**

<img width="622" height="239" alt="Image" src="https://github.com/user-attachments/assets/2eb3fb90-89bd-4191-8582-228203e9b9fd" />

**SETTINGS CHANGED IN SETTINGS.XML FILE**

<img width="585" height="752" alt="Image" src="https://github.com/user-attachments/assets/0eeffc36-1708-42cf-a70e-645dded0bd2e" />

**MVN DEPLOY SUCCESS**

<img width="1301" height="403" alt="Image" src="https://github.com/user-attachments/assets/444933a9-e47b-4d54-9532-ae2cd20c8399" />

**WAR-FILE UPLOADED SUCCESSFULLY**

<img width="1589" height="837" alt="Image" src="https://github.com/user-attachments/assets/f67d9b78-3708-4f87-8ecb-f3be107475a5" />
### Deploy Server

Purpose: Deploy .war file from Nexus to Tomcat.


**CONNECT TO-DEPLOY SERVER**

<img width="983" height="122" alt="Image" src="https://github.com/user-attachments/assets/e7d3ea14-d6f4-46e7-bf7f-b05375766a88" />

**VALVE-BLOCK IN-HOSTMANAGER-IN DEPLOY SERVER**

<img width="1599" height="705" alt="Image" src="https://github.com/user-attachments/assets/79df15ed-8a7d-44c2-8cd6-677cb0062082" />

**GO TO-CONTENT.XML FILE IN DEPLOY SERVER**

<img width="1349" height="364" alt="Image" src="https://github.com/user-attachments/assets/07398285-7643-4030-ae18-b161f93b91b6" />

**AGAIN GO TO CONTENT.XML2 FILE**

<img width="876" height="188" alt="Image" src="https://github.com/user-attachments/assets/68abf18e-2c37-4f11-a7c4-dcce594458eb" />

**CHANGED**

<img width="1599" height="157" alt="Image" src="https://github.com/user-attachments/assets/49c07f8a-9487-43ac-9604-05d458e89e82" />

**NOW GO TO TOMCAT USER.XML FILE**

<img width="1595" height="180" alt="Image" src="https://github.com/user-attachments/assets/a6033bac-90a6-4540-85ee-ee6f5ccbc539" />

**TOMCAT-USER-CREDENTILAS-UPDATED**

<img width="1549" height="839" alt="Image" src="https://github.com/user-attachments/assets/3aec830c-5758-425d-9ee3-6de166e1a8ff" />

**TOMCAT-STARTED**

<img width="1599" height="166" alt="Image" src="https://github.com/user-attachments/assets/45c07b67-7aaf-4a52-9cfc-71cff77b59d4" />


**END TO END WORKFLOW**

**WGET TO DOWNLOAD THE ARTIFACT TO THE DEPLOY SERVER**

<img width="1477" height="347" alt="Image" src="https://github.com/user-attachments/assets/b3be2780-5623-4489-b27b-15690000582f" />

**ARTIFACT CAME TO TOMCAT**

<img width="1565" height="805" alt="Image" src="https://github.com/user-attachments/assets/ed7ce96b-b040-4678-97b3-99f42cc90b1e" />

**DEPLOYED SUCCESSFULLY**

<img width="1205" height="451" alt="Image" src="https://github.com/user-attachments/assets/4861448d-cda1-45d7-99d2-e7975ffb969d" />

**OUTPUT**

<img width="1040" height="516" alt="Image" src="https://github.com/user-attachments/assets/ffd065c7-61b9-42c4-90ab-76f603615638" />




✅ Final Deliverables

### OUTPUT IMAGES
**1**


<img width="1205" height="451" alt="Image" src="https://github.com/user-attachments/assets/4e622a7b-30f3-4204-b31f-a74a162f4473" />

**2**



