# Multi-Server Java Application Build, Store, and Deployment System

## 🎯 Objective
The goal of this task is to set up and configure a **multi-server environment** for building, storing, and deploying a **Java web application** using **JFrog Artifactory** as the artifact repository.  
This project follows a CI/CD-style workflow across three servers:

- **Java Build Server:** To build the Java web application.
- **JFrog Artifactory Server:** To store the generated `.war` artifacts.
- **Deploy Server:** To deploy the application using Apache Tomcat.

The setup ensures smooth communication between all three servers for an automated and reliable deployment process.

---

## 🧩 Requirements

- **GitHub Repository:**  
  Java Web Calculator App – [https://github.com/mrtechreddy/Java-Web-Calculator-App.git](https://github.com/mrtechreddy/Java-Web-Calculator-App.git)

- **Three Servers:**
  1. Java Build Server  
  2. JFrog Artifactory Repository Server  
  3. Deploy Server (Tomcat)

---

## 🖥️ 1. Java Build Server Setup

### Overview
The Build Server is responsible for cloning the Java Web Calculator project, building it using Maven, and uploading the generated `.war` file to JFrog Artifactory.

### Steps

1. **Clone the Project**  
   Obtain the Java Web Calculator App source code from the provided GitHub repository.

2. **Build the Application**  
   Use **Apache Maven** to build the project and generate the `.war` file in the `target/` directory.

3. **Configure Maven for Deployment**  
   Modify the `pom.xml` and Maven `settings.xml` files to include:
   - The **JFrog repository URL**
   - **Authentication credentials** (username and password/API key)

4. **Deploy the Artifact**  
   After a successful build, deploy the `.war` file to JFrog Artifactory using Maven deployment configuration.

### Deliverables
- Cloned Java Web Calculator project directory on the Build Server  
- `.war` file generated in the `target/` directory  
- Successfully uploaded artifact in the JFrog repository  

---

## 🗄️ 2. JFrog Artifactory Server Setup

### Overview
The JFrog Artifactory Server acts as the **central artifact repository** where build artifacts such as `.war` files are stored and managed.

### Steps

1. **Install JFrog Artifactory**  
   Set up JFrog Artifactory OSS or Pro version on the designated server. Ensure that the Artifactory web console is accessible from both the build and deploy servers.

2. **Create Repositories**  
   Configure Maven repositories in JFrog:
   - **Release Repository** for production-ready builds  
   - **Snapshot Repository** for ongoing development builds  

3. **Set Up Authentication**  
   Configure user accounts and permissions for both uploading and downloading artifacts.  
   Update the Maven `settings.xml` files on build and deploy servers with the required credentials.

4. **Monitor Artifactory**  
   Verify that:
   - The repository is accessible from the build server  
   - Artifacts are uploaded successfully  
   - Sufficient disk space and repository health are maintained  

### Deliverables
- JFrog Artifactory server running and accessible  
- Configured repositories for releases and snapshots  
- Authentication successfully tested between build and deploy servers  
- Uploaded `.war` file visible in the JFrog UI  

---

## 🚀 3. Deploy Server Setup

### Overview
The Deploy Server hosts the Java web application by fetching the `.war` file from JFrog Artifactory and deploying it using **Apache Tomcat**.

### Steps

1. **Install Apache Tomcat**  
   Configure Apache Tomcat as the application server for hosting the Java Web Calculator App.

2. **Fetch Artifact from JFrog**  
   Configure a Maven or custom script to download the `.war` file from JFrog Artifactory using repository URL and credentials.

3. **Automate Deployment**  
   Copy the `.war` file to the Tomcat `webapps/` directory.  
   Start or restart Tomcat to automatically deploy the application.

4. **Test the Application**  
   Access the application in a web browser using:  
   `http://<DEPLOY_SERVER_IP>:8080/<artifact-name>`