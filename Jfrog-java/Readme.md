# 🧰 Multi-Server Java Web Application Build, Store, and Deployment System (JFrog Artifactory)

## 🎯 Objective
This project demonstrates how to set up a **multi-server environment** for building, storing, and deploying a **Java Web Application** using **JFrog Artifactory** as the artifact repository.

The system consists of **three servers**:
1. **Java Build Server** → Build and upload the `.war` file to JFrog Artifactory  
2. **JFrog Repository Server** → Store and manage build artifacts  
3. **Deploy Server** → Download and deploy the application to Apache Tomcat  

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
bash
Copy code
java -version
mvn -version
git --version
Step 3: Clone the Project
bash
Copy code
git clone https://github.com/mrtechreddy/Java-Web-Calculator-App.git
cd Java-Web-Calculator-App
Step 4: Build the Project
bash
Copy code
mvn clean install
✅ This generates the .war file under the target/ directory.

📦 2️⃣ JFrog Repository Server Setup
Step 1: Install JFrog Artifactory OSS
bash
Copy code
sudo apt update -y
wget https://releases.jfrog.io/artifactory/artifactory-debs/pool/jfrog-artifactory-oss/jfrog-artifactory-oss-7.104.12.deb
sudo dpkg -i jfrog-artifactory-oss-7.104.12.deb
Step 2: Start and Enable JFrog Service
bash
Copy code
sudo systemctl start artifactory
sudo systemctl enable artifactory
Step 3: Access JFrog UI
Open your browser and visit:

arduino
Copy code
http://<JFROG_SERVER_IP>:8082/ui/
Step 4: Create Maven Repositories
In the JFrog UI:

Go to Administration → Repositories → Local

Click New Local Repository

Choose Maven → Release

Name it java-web-release

Save it

Copy the repository URL, e.g.:

arduino
Copy code
http://<JFROG_SERVER_IP>:8081/artifactory/java-web-release
⚙️ 3️⃣ Configure Maven for JFrog Deployment
Step 1: Update pom.xml
Add this section inside <distributionManagement>:

xml
Copy code
<distributionManagement>
    <repository>
        <id>jfrog-release</id>
        <url>http://<JFROG_SERVER_IP>:8081/artifactory/java-web-release</url>
    </repository>
</distributionManagement>
Step 2: Configure Maven credentials in ~/.m2/settings.xml
bash
Copy code
vim ~/.m2/settings.xml
Add the following:

xml
Copy code
<settings>
  <servers>
    <server>
      <id>jfrog-release</id>
      <username>admin</username>
      <password><your_admin_password></password>
    </server>
  </servers>
</settings>
Step 3: Deploy Artifact to JFrog
bash
Copy code
mvn deploy
✅ This uploads the .war file to JFrog Artifactory under java-web-release.

Step 4: Verify Upload
In JFrog UI → Repositories → java-web-release → check for your .war file.

🌐 4️⃣ Deploy Server Setup
Step 1: Install Apache Tomcat
bash
Copy code
sudo apt update -y
sudo apt install tomcat9 tomcat9-admin -y
Step 2: Verify Tomcat is running
bash
Copy code
sudo systemctl status tomcat9
Access in browser:

cpp
Copy code
http://<DEPLOY_SERVER_IP>:8080
Step 3: Download .war file from JFrog
bash
Copy code
cd /tmp
wget --user=admin --password=<your_admin_password> \
"http://<JFROG_SERVER_IP>:8081/artifactory/java-web-release/JavaWebCalculatorApp/1.0/JavaWebCalculatorApp-1.0.war" \
-O JavaWebCalculatorApp.war
Step 4: Deploy the .war to Tomcat
bash
Copy code
sudo cp JavaWebCalculatorApp.war /var/lib/tomcat9/webapps/
sudo systemctl restart tomcat9
Step 5: Access the Application
Open your browser:

cpp
Copy code
http://<DEPLOY_SERVER_IP>:8080/JavaWebCalculatorApp
🔁 5️⃣ End-to-End Testing
✅ Build & Upload from Build Server
bash
Copy code
mvn clean install
mvn deploy
✅ Verify in JFrog Artifactory
Check the uploaded artifact in:

ruby
Copy code
http://<JFROG_SERVER_IP>:8082/ui/repos/tree/General/java-web-release
✅ Download & Deploy on Deploy Server
bash
Copy code
wget --user=admin --password=<your_admin_password> \
"http://<JFROG_SERVER_IP>:8081/artifactory/java-web-release/JavaWebCalculatorApp/1.0/JavaWebCalculatorApp-1.0.war" \
-O JavaWebCalculatorApp.war

sudo cp JavaWebCalculatorApp.war /var/lib/tomcat9/webapps/
sudo systemctl restart tomcat9
✅ Test in Browser
cpp
Copy code
http://<DEPLOY_SERVER_IP>:8080/JavaWebCalculatorApp
If you see the Java Web Calculator interface — 🟢 Congratulations!
Your multi-server CI/CD pipeline using JFrog Artifactory is complete.
