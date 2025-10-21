# Java 8 Installation and SonarQube Setup Guide

This document provides the full set of commands executed on the
`java-sonar` server for installing Java 8, cloning a Java project, and
performing SonarQube analysis.

------------------------------------------------------------------------

## 🧰 Command History with Explanations

1.  **Change Hostname**

    ``` bash
    sudo vi /etc/hostname
    ```

    Opens the hostname configuration file for editing.

2.  **Restart System**

    ``` bash
    sudo init 6
    ```

    Reboots the server to apply the new hostname.

3.  **Check Java Version**

    ``` bash
    java -version
    ```

    Verifies if Java is already installed.

4.  **Update Package Repository**

    ``` bash
    sudo apt update
    ```

    Updates the list of available packages and their versions.

5.  **Install Java 8 (JDK 8)**

    ``` bash
    sudo apt install openjdk-8-jdk -y
    ```
    <img width="1448" height="641" alt="instance" src="https://github.com/user-attachments/assets/f2adaec7-854c-4da4-b286-742902f8fb47" />


<img width="1335" height="235" alt="oprt-9000" src="https://github.com/user-attachments/assets/d6b44a7c-90ef-4041-9a49-5db53719eb9c" />


<img width="1522" height="356" alt="ssh connect" src="https://github.com/user-attachments/assets/8aa0101a-cf56-44f4-90c7-cd6d85919a71" />

6.  **List Installed Java Versions**

    ``` bash
    sudo update-alternatives --list java
    ```

    Displays all available Java installations.

7.  **Switch Java Version**

    ``` bash
    sudo update-alternatives --config java
    ```

    Allows selection of Java 8 as the default version.

8.  **Verify Java Version**

    ``` bash
    java -version
    ```

    Confirms the active Java version.

9.  **Clone Java Project from GitHub**

    ``` bash
    git clone https://github.com/akracad/JavaWebCalculator.git
    ```
    <img width="1221" height="379" alt="git-clone" src="https://github.com/user-attachments/assets/bf67698a-989d-4e92-bb0d-e4d973795400" />



10. **Build the Maven Project**
    ```
    cd JavaWebCalculator/
      mvn package
    ```
    <img width="1599" height="446" alt="install maven" src="https://github.com/user-attachments/assets/4a494523-a9cf-4ab3-a2d2-c7c16f7480fe" />

    <img width="1593" height="413" alt="mvn-package" src="https://github.com/user-attachments/assets/51668e09-0865-4f16-a9bf-6768b94fdc21" />


    Builds the Java
    project and creates a `.war` file.

12. **Start SonarQube Server**
    ```
    ~/sonarqube-6.7.7/bin/linux-x86-64
        ./sonar.sh start
      ./sonar.sh status`
    ```
    Starts SonarQube and checks its status.

    <img width="1595" height="551" alt="install-sonar-cube" src="https://github.com/user-attachments/assets/bcde5b16-bf23-4ad0-a672-5aa7f6bed587" />

    <img width="1107" height="346" alt="unzip" src="https://github.com/user-attachments/assets/33134dd7-6f9f-4b08-9a6b-af061a972d55" />



    <img width="1599" height="717" alt="start sonarcube" src="https://github.com/user-attachments/assets/bcd384f6-ad9a-47d8-ac1f-6336c5a5d372" />

    <img width="1277" height="525" alt="welcome to sonarcube" src="https://github.com/user-attachments/assets/6ac2b22c-616c-4924-af94-0f9914b4fb8b" />



14. **Run SonarQube Analysis**
    ```
    mvn sonar:sonar
    
    -Dsonar.host.url=http://98.81.81.192:9000
    -Dsonar.login=75cd7bddcc65146c5bfabae1f4377c834feb3885
    ```
    Runs code quality analysis using Maven and SonarQube.

    <img width="1282" height="541" alt="copy-link" src="https://github.com/user-attachments/assets/8e007a65-8eab-4e1c-8d39-6f5317be3050" />

    <img width="1599" height="899" alt="ootput" src="https://github.com/user-attachments/assets/5357cc48-acfc-4b35-9c0e-054a1e4361a3" />


<img width="1589" height="899" alt="output2" src="https://github.com/user-attachments/assets/08a7a301-f680-425b-8521-6af045bd6b05" />



16. **Edit `pom.xml` (if required)**
    ```
    sudo vi pom.xml
   ```
   Used for
    adjusting configurations such as plugin details.
    ```
        ------------------------------------------------------------------------
```
## ✅ Summary

You have: - Installed **Java 8** - Built a **Java Maven project** -
Configured and analyzed code with **SonarQube**

------------------------------------------------------------------------

**Author:** Pawankumar\
**Environment:** Ubuntu Server (java-sonar)\
**Tools Used:** Java 8, Maven, Git, SonarQube 6.7.7
