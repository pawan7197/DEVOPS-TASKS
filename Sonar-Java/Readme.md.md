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

    Installs OpenJDK 8 which includes both JRE and development tools.

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

    Downloads the Java web calculator project.

10. **Build the Maven Project**
    `bash     cd JavaWebCalculator/     mvn package` Builds the Java
    project and creates a `.war` file.

11. **Start SonarQube Server**
    `bash     cd ~/sonarqube-6.7.7/bin/linux-x86-64     ./sonar.sh start     ./sonar.sh status`
    Starts SonarQube and checks its status.

12. **Run SonarQube Analysis**
    `bash     mvn sonar:sonar       -Dsonar.host.url=http://98.81.81.192:9000       -Dsonar.login=75cd7bddcc65146c5bfabae1f4377c834feb3885`
    Runs code quality analysis using Maven and SonarQube.

13. **Edit `pom.xml` (if required)** `bash     sudo vi pom.xml` Used for
    adjusting configurations such as plugin details.

------------------------------------------------------------------------

## ✅ Summary

You have: - Installed **Java 8** - Built a **Java Maven project** -
Configured and analyzed code with **SonarQube**

------------------------------------------------------------------------

**Author:** Pawankumar\
**Environment:** Ubuntu Server (java-sonar)\
**Tools Used:** Java 8, Maven, Git, SonarQube 6.7.7
