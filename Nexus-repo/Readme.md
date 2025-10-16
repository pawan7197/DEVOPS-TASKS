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
```
wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz

```
**EXTRACT-FILE**

<img width="1419" height="123" alt="Image" src="https://github.com/user-attachments/assets/61366fcb-ff14-433f-ab30-5692be5cd157" />

```
tar -xvf latest-unix.tar.gz
```

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


### Deploy Server

Purpose: Deploy .war file from Nexus to Tomcat.

Steps:
```
Install Apache Tomcat


sudo apt install tomcat9 -y
```

Download artifact from Nexus


```
wget http://<NEXUS_SERVER_IP>:8081/repository/maven-releases/com/example/JavaWebCalculator/<version>/JavaWebCalculator-<version>.war

```

Deploy to Tomcat

```
sudo cp JavaWebCalculator-<version>.war /var/lib/tomcat9/webapps/
sudo systemctl restart tomcat9

```

Test the application

```
http://<DEPLOY_SERVER_IP>:8080/JavaWebCalculator
```

Deliverables:
```
Tomcat running the Java Web Calculator app
```


Application accessible via web browser

### End-to-End Workflow

Build server runs:

```
mvn clean install
mvn deploy
```


```
Nexus receives and stores the .war file
```


```
Deploy server fetches the .war from Nexus and deploys it to Tomcat
```

Access application at:

```
http://<DEPLOY_SERVER_IP>:8080/JavaWebCalculator
```
✅ Final Deliverables

### OUTPUT IMAGES


