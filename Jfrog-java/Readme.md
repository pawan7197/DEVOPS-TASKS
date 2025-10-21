# 🧰 Multi-Server Java Web Application Build, Store, and Deployment System (JFrog Artifactory)

## 🎯 Objective
This project demonstrates how to set up a **multi-server environment** for building, storing, and deploying a **Java Web Application** using **JFrog Artifactory** as the artifact repository.

The system consists of **three servers**:
1. **Java Build Server** → Build and upload the `.war` file to JFrog Artifactory  
2. **JFrog Repository Server** → Store and manage build artifacts  
3. **Deploy Server** → Download and deploy the application to Apache Tomcat  

***Three servers***

<img width="1599" height="656" alt="instances" src="https://github.com/user-attachments/assets/a00aadff-460f-4e45-a0ec-0c41c31a0a11" />

---

## 🖥️ Prerequisites
- Three Ubuntu servers (Build, JFrog, Deploy)
- Java 17+
- Apache Maven
- Git
- Apache Tomcat (on Deploy server)
- JFrog Artifactory OSS (on JFrog server)

---

## 🚀 1️⃣ Java Build Server Setup

### Step 1: Update and Install Java + Maven + Git
```
sudo apt update -y
sudo apt install openjdk-17-jdk maven git -y
```
Step 2: Verify installations
```
java -version
mvn -version
git --version
```
Step 3: Clone the Project
```
git clone https://github.com/mrtechreddy/Java-Web-Calculator-App.git
cd Java-Web-Calculator-App
```
Step 4: Build the Project
```
mvn clean install
```

## 2️⃣ JFrog Repository Server Setup

Step 1: Install JFrog Artifactory 
```
sudo apt update -y
wget https://releases.jfrog.io/artifactory/artifactory-debs/pool/jfrog-artifactory-oss/jfrog-artifactory-oss-7.104.12.deb
sudo dpkg -i jfrog-artifactory-oss-7.104.12.deb
```
Step 2: Start and Enable JFrog Service
```
sudo systemctl start artifactory
sudo systemctl enable artifactory
```
Step 3: Access JFrog UI
Open your browser and visit:

```
http://<JFROG_SERVER_IP>:8082/ui/
```
***accessing Jfrog***
<img width="1599" height="654" alt="Jfrog opening1" src="https://github.com/user-attachments/assets/677c7d10-816d-4055-ba88-5656e72a20f4" />

***Jfrog-login page***

<img width="1556" height="704" alt="login page2" src="https://github.com/user-attachments/assets/5127b52e-595a-486d-902a-aafbaf502459" />

***Login-success***
<img width="1599" height="724" alt="login success 3" src="https://github.com/user-attachments/assets/43f20ae5-ad7e-4bd7-9863-d53a0e96afc1" />

***Create a local repo***
<img width="1544" height="432" alt="create local repo 4" src="https://github.com/user-attachments/assets/78fa1d85-2c03-4d32-85b9-cf91343f140a" />

***repo-created***
<img width="1593" height="527" alt="repo created 5" src="https://github.com/user-attachments/assets/f94f2ed7-8b18-40f3-b0ee-8b9aa2877900" />

***Copy the URL of repo***
<img width="1586" height="640" alt="copy the URL of repo 6" src="https://github.com/user-attachments/assets/5ddddb2e-2868-4002-8f06-8368d6b8d2b7" />

***Copy the repo URL and ID in pom.xml***
<img width="1599" height="837" alt="copy the repo URL and ID in POM XML at distribution management" src="https://github.com/user-attachments/assets/ddd4a3ef-cc08-4727-8d68-0dabfe91499e" />

***now open the settings.xml file on build-server***

<img width="753" height="146" alt="now go to settings xml file 8" src="https://github.com/user-attachments/assets/852fea4e-4f2c-480f-ab43-92a9ab898749" />

***credentials updated in settings.xml on build server**

<img width="1595" height="835" alt="setting xml file credentilas update 9" src="https://github.com/user-attachments/assets/3ecfe061-0d45-4df7-9c02-1cbead872a20" />

***artifact in Jfrog***

<img width="1578" height="687" alt="artifact in Jfrog 10" src="https://github.com/user-attachments/assets/e93f1401-38b3-4e80-86b7-41626eab7558" />



## 🌐 4️⃣ Deploy Server Setup

Step 1: Install Apache Tomcat
```
sudo apt update -y
sudo apt install tomcat9 tomcat9-admin -y
Step 2: Verify Tomcat is running
```
sudo systemctl status tomcat9
Access in browser:

```
http://<DEPLOY_SERVER_IP>:8080
```
Step 3: Download .war file from JFrog
```
cd /tmp
wget --user=admin --password=<your_admin_password> \
"http://<JFROG_SERVER_IP>:8081/artifactory/java-web-release/JavaWebCalculatorApp/1.0/JavaWebCalculatorApp-1.0.war" \
-O JavaWebCalculatorApp.war
```
Step 4: Deploy the .war to Tomcat
```
sudo cp JavaWebCalculatorApp.war /var/lib/tomcat9/webapps/
sudo systemctl restart tomcat9
```
Step 5: Access the Application
Open your browser:

```
http://<DEPLOY_SERVER_IP>:8080/JavaWebCalculatorApp

```

***open the context.xml file***

<img width="1315" height="461" alt="go to context xml file" src="https://github.com/user-attachments/assets/36621d8e-6e03-4e0b-8374-29f28c8702bc" />


***valve block in conext.xml file***

<img width="1599" height="751" alt="conetxt xml block valve in deploy server 11" src="https://github.com/user-attachments/assets/10646629-11ed-45da-a3db-1f972af7212f" />

***go to context.xml file in manager***

<img width="923" height="169" alt="no again goto manager to context xml file 12" src="https://github.com/user-attachments/assets/671c5f19-7dce-416e-854e-bd8d866272f0" />

***context.xml file in manager***

<img width="1599" height="532" alt="context xml in manager file 13" src="https://github.com/user-attachments/assets/dc2cde45-27fa-4591-a607-6f9cbc3791fd" />

***Edit conf file***

<img width="1575" height="210" alt="edit conf file 14" src="https://github.com/user-attachments/assets/774d1fad-8466-48ea-926c-a393c61d60df" />

***add script***

<img width="1334" height="841" alt="add script 15" src="https://github.com/user-attachments/assets/3c60f95c-a1f8-44b1-8d34-52b25f1acd4b" />

***copy the repo path***

<img width="1591" height="714" alt="copy the Repo path 15 1" src="https://github.com/user-attachments/assets/7ecdb584-c9f0-4f7f-9777-123da02f26c1" />


***copy the repo path in Webapp***

<img width="1584" height="587" alt="copy the repo path in webapp 16" src="https://github.com/user-attachments/assets/1970115c-b9cd-4dd1-a313-f183101f9372" />

***Test in browser***

<img width="1463" height="291" alt="output 17" src="https://github.com/user-attachments/assets/033c6d8f-4261-45a7-b328-763f9799918a" />

***output***

<img width="1302" height="736" alt="output 18" src="https://github.com/user-attachments/assets/be0862a6-2561-4927-8469-209db222fb2d" />




🔁 5️⃣ End-to-End Testing
✅ Build & Upload from Build Server

```
mvn clean install
mvn deploy
```
✅ Verify in JFrog Artifactory
Check the uploaded artifact in:

```
http://<JFROG_SERVER_IP>:8082/ui/repos/tree/General/java-web-release
```
✅ Download & Deploy on Deploy Server
```
wget --user=admin --password=<your_admin_password> \
"http://<JFROG_SERVER_IP>:8081/artifactory/java-web-release/JavaWebCalculatorApp/1.0/JavaWebCalculatorApp-1.0.war" \
-O JavaWebCalculatorApp.war

sudo cp JavaWebCalculatorApp.war /var/lib/tomcat9/webapps/
sudo systemctl restart tomcat9
```
✅ Test in Browser
```
http://<DEPLOY_SERVER_IP>:8080/JavaWebCalculatorApp
```
If you see the Java Web Calculator interface — 🟢 Congratulations!
Your multi-server CI/CD pipeline using JFrog Artifactory is complete.
