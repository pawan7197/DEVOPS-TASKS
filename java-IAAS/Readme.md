## LoginWebApp: Java + MySQL Web Application on Tomcat using AWS RDS(IAAS):


This project is a **Java-based web application** that provides user registration and login functionality. It uses **MySQL hosted on AWS RDS** for database storage and is deployed on **Apache Tomcat**. This project demonstrates integrating a Java backend with a cloud-hosted database and deploying a complete web application.

---

## 🧩 Features:


- User registration with unique username and email
- Secure login functionality
- Integration with **AWS RDS MySQL database**
- Deployed on **Apache Tomcat server**
- Easy-to-understand Java + JSP + Servlet code structure

---

## 📂 Project Structure:


```
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
pom.xml: Maven project configuration and dependencies

WEB-INF/web.xml: Servlet mappings and configurations

JSP pages: Frontend for user login, registration, and welcome screens

## 🪜 Step-by-Step Deployment Instructions:

## 1️⃣ Clone the Project:

```
git clone https://github.com/mrtechreddy/aws-rds-java.git
cd LoginWebApp
```
## 2️⃣ Create MySQL Database on AWS RDS(IAAS):

```
mysql -h <your-ip-address> -u admin -p  
```

## 3️⃣ Create Required Table:

**Connect to your RDS MySQL instance via CLI:**

```
mysql -h <your-ip-address> -u admin -p
```
**Run the following SQL:**

```
CREATE DATABASE jwt;
USE jwt;
```
```
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
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci;
```
## 4️⃣ Update Database Credentials in the Code:

Edit login.jsp and userRegistration.jsp:

```
String jdbcURL = "jdbc:mysql://<your-rds-endpoint>:3306/jwt?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC";
String dbUser = "admin";
String dbPass = "admin123";
```
Replace <your-ip-address> with your actual ip address.

## 5️⃣ Build the WAR File Using Maven:

**From the project root:**

```
mvn clean package
```

**After a successful build, you’ll get:**

```
target/LoginWebApp.war
```

## 6️⃣ Deploy to Apache Tomcat:

**Copy the WAR file to Tomcat’s webapps directory:**

```
sudo cp target/LoginWebApp.war /opt/tomcat/webapps/
```
**Restart Tomcat:**

```
sudo systemctl restart tomcat
```
# OR if running manually
```
/opt/tomcat/bin/shutdown.sh
/opt/tomcat/bin/startup.sh
```
**Access the app in your browser:**

```
http://<EC2-public-ip>:8080/LoginWebApp/
```

## 7️⃣ Test Your Deployment:

Open the app → Register a new user

Verify the data in your RDS table

Log in using the same credentials

Confirm successful redirection to success.jsp or welcome.jsp

## 🧠 Bonus Challenges:

Use environment variables to secure DB credentials instead of hardcoding

Deploy Tomcat on an EC2 instance inside the same VPC as RDS for secure connectivity

Add SSL using Nginx reverse proxy on port 443

Automate deployment using Jenkins or GitHub Actions

## ✅ Deliverables:

## Screenshot of login page running on Tomcat:


## Screenshot of user data in AWS RDS:


## Screenshot of successful registration/login

## Author:

**Pawan Kumar Kothapalli**

**Devops Engineer**

**Mail-Id:** pawankumarkothapalli22644@gmail.com

**LinkedIn** 