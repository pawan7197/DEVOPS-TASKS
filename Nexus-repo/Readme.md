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

<img width="611" height="215" alt="buildserver connect" src="https://github.com/user-attachments/assets/74852653-ae26-4acb-b630-e421758d8d89" />



#### Steps:
1. **Clone the project**
   ```bash
   git clone https://github.com/mrtechreddy/Java-Web-Calculator-App.git
   cd Java-Web-Calculator-App
Build the application

``
mvn clean install
✅ This generates a .war file inside the target/ directory.
``

Configure Maven for Nexus Deployment
```

Edit pom.xml → add <distributionManagement> section with Nexus URL.

Edit ~/.m2/settings.xml → add Nexus credentials.
```

Deploy artifact to Nexus

```
mvn deploy
```
Deliverables:
```
.war file created in target/
```

Artifact successfully uploaded to Nexus Repository

### Nexus Repository Server:


Purpose: Store and manage build artifacts (.war files)

Steps:
```
Install Nexus Repository Manager
```
```
wget https://download.sonatype.com/nexus/3/latest-unix.tar.gz
tar -xvf latest-unix.tar.gz
cd nexus-3*
./bin/nexus start
Access Nexus UI:
http://<NEXUS_SERVER_IP>:8081
```

Create Repositories:

maven-releases



Set up authentication:
```
Create a new user for build and deploy servers.

Update Maven credentials in settings.xml.
```

Deliverables:

```
Nexus server up and running
```

Repositories configured and accessible

```
Verified .war upload from build server
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


