## Deploy Java + MySQL Web Application on Tomcat using AWS RDS##

This project demonstrates how to **deploy a complete Java-based Login Web Application** connected to a **MySQL database hosted on AWS RDS**, and run it on **Apache Tomcat** hosted on an **EC2 instance**.

---

## 🧩 Objective

To integrate backend Java code, configure a managed MySQL database on AWS RDS, and deploy the application on Apache Tomcat, validating the full workflow — from code build to database connectivity and live access.

---

## 🪜 Step-by-Step Implementation Guide

### 1️⃣ Clone the Project
```bash
git clone https://github.com/mrtechreddy/aws-rds-java.git
cd LoginWebApp
2️⃣ Review Project Structure

LoginWebApp/
├── pom.xml
└── src/
    └── main/
        └── webapp/
            ├── WEB-INF/web.xml
            ├── index.jsp
            ├── login.jsp
            ├── register.jsp
            ├── userRegistration.jsp
            ├── success.jsp
            └── welcome.jsp
 ```           
3️⃣ Setup AWS RDS (MySQL)
```
a. Create the RDS instance
Engine: MySQL 8.x

Template: Free Tier

DB Identifier: jwt

Username: admin

Password: admin123

Public Access: ✅ Enabled

VPC Security Group: Allow inbound 3306 from EC2 or your local IP
```
Example RDS endpoint:
```
database-1.c878m284ssbq.us-east-1.rds.amazonaws.com
```
4️⃣ Create Database & Table
Connect to RDS:
```
mysql -h <your-rds-endpoint> -u admin -p
Run:


CREATE DATABASE jwt;
USE jwt;

CREATE TABLE `USER` (
  `id` INT UNSIGNED NOT NULL AUTO_INCREMENT,
  `first_name` VARCHAR(100) NOT NULL,
  `last_name` VARCHAR(100) NOT NULL,
  `email` VARCHAR(150) NOT NULL,
  `username` VARCHAR(100) NOT NULL,
  `password` VARCHAR(255) NOT NULL,
  `regdate` DATE NOT NULL,
  PRIMARY KEY (`id`),
  UNIQUE KEY `unique_username` (`username`),
  UNIQUE KEY `unique_email` (`email`)
) ENGINE=InnoDB 
  DEFAULT CHARSET=utf8mb4 
  COLLATE=utf8mb4_unicode_ci;
  ```
5️⃣ Update Database Configuration in Code
Edit login.jsp and userRegistration.jsp:
```

java

String jdbcURL = "jdbc:mysql://<your-rds-endpoint>:3306/jwt?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC";
String dbUser = "admin";
String dbPass = "admin123";
Replace <your-rds-endpoint> with your actual RDS endpoint.

```
6️⃣ Build the Project using Maven
```

mvn clean package
WAR file will be generated at:

Copy code
target/LoginWebApp.war

```
7️⃣ Deploy to Apache Tomcat
```
Copy WAR to Tomcat webapps:


sudo cp target/LoginWebApp.war /opt/tomcat/webapps/


Restart Tomcat:

sudo systemctl restart tomcat



/opt/tomcat/bin/shutdown.sh
/opt/tomcat/bin/startup.sh
Access the app:


http://<EC2-public-ip>:8080/LoginWebApp/

```
8️⃣ Test the Application
```
Register a new user.

Verify data in RDS:

sql

SELECT * FROM USER;
Log in using the same credentials.

Confirm redirection to success.jsp or welcome.jsp.

## IMAGES:

## 1.Java build server

<img width="1599" height="765" alt="javabuild-server 1" src="https://github.com/user-attachments/assets/7438d065-8efb-43ee-b184-0e7f902315ac" />

## 2.Hostname changed

<img width="475" height="44" alt="hostname changed 2" src="https://github.com/user-attachments/assets/c59b00ca-1e4a-46b4-b601-db7ad0e79910" />

## 3.Clone the code

<img width="734" height="265" alt="git clone 3" src="https://github.com/user-attachments/assets/5304f338-82ba-4ef6-b2ef-67e79ac579ad" />

## 4. Install Java

<img width="915" height="138" alt="java installe 4" src="https://github.com/user-attachments/assets/6803caed-6916-45da-b53a-28873a30dcbc" />

## 5.Build success

<img width="786" height="261" alt="buil success 5" src="https://github.com/user-attachments/assets/6d3e3103-b3e4-4f52-9ccb-ef2e9cd68fa9" />

## 6.MVN versioning

<img width="848" height="185" alt="mvn version 6" src="https://github.com/user-attachments/assets/ecb58712-d520-425d-9f1b-fa00009304f8" />


## 7.AWS Database created

<img width="1599" height="747" alt="AWS database created 7" src="https://github.com/user-attachments/assets/cdea95e1-28e4-4808-b235-064449ee5ce3" />

## 8.database endpoint created

<img width="1599" height="853" alt="database endpoint configured 8" src="https://github.com/user-attachments/assets/3345d904-969d-4ae0-88bb-34442ad1659e" />


## 9.endpoint configured in user registration

<img width="1567" height="836" alt="endpoint pasted in user registration 9 " src="https://github.com/user-attachments/assets/40e337e9-3deb-45bf-b880-3e47f55fcef0" />


## 10. Deploy server

<img width="1574" height="726" alt="java-deploy-server 10" src="https://github.com/user-attachments/assets/d6f73481-f52c-4113-9085-3000d5a48ac6" />


## 11. Apache tomcat installation

<img width="1108" height="93" alt="apache-tomcat install" src="https://github.com/user-attachments/assets/30b73562-5a33-426a-a3e2-a53bd4a6cd3f" />

## 12. Tomcat configuration

<img width="1592" height="573" alt="tomcat-configuration" src="https://github.com/user-attachments/assets/ac3842b4-4e7d-4a7a-b532-a6c7d9f6e8f9" />


## 13. Install java in tomcat

<img width="1591" height="400" alt="Java in tomcat" src="https://github.com/user-attachments/assets/0b108af9-5a84-4549-a9e2-d69842d1cf73" />

## 14. Registration and login

<img width="1286" height="731" alt="registration and login" src="https://github.com/user-attachments/assets/8becfda0-0959-4b77-b1a1-2ce1fe45d803" />

## 15. Create database

<img width="1179" height="501" alt="create database" src="https://github.com/user-attachments/assets/ac6a0be5-c706-4bca-80c3-aeb719adce9c" />

## 16. login to database

<img width="1417" height="807" alt="login to database" src="https://github.com/user-attachments/assets/c6061db7-4227-4d7b-8579-7bf3282b9006" />

## 17. Output

<img width="1354" height="333" alt="Image" src="https://github.com/user-attachments/assets/5989d009-d824-4717-a8ae-6043ae983df3" />



