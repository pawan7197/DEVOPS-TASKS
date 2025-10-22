# Javascript-Sonarcube

This repository contains a simple Angular Calculator application. This guide also includes all steps to perform **SonarQube analysis** with proper bash commands.

---

## Table of Contents

- [Project Setup](#project-setup)
- [Run Angular Application](#run-angular-application)
- [SonarQube Setup](#sonarqube-setup)
- [SonarQube Analysis](#sonarqube-analysis)
- [Author](#author)

---

## Project Setup

### 1. Clone the Project


# Clone the Angular project from GitHub
```
git clone https://github.com/mrtechreddy/Angular-Calc-App.git
```
# Go into the project directory
```
cd Angular-Calc-App
```

# Install Java 8

```
sudo apt install openjdk-8-jdk -y

```
2. Install Dependencies
# Install all required Node.js packages
```
npm install
Run Angular App
```

# Run the Angular development server
```
ng serve
Open your browser at: http://localhost:4200
```
SonarQube Setup
1. Make Sure SonarQube is Running

# Go to SonarQube installation folder
```
cd ~/sonarqube-6.7.7/bin/linux-x86-64

```

# Make sure sonar.sh is executable

```
sudo chmod +x sonar.sh
```

# Start SonarQube server
```
./sonar.sh start
```

# Check status of SonarQube server
```
./sonar.sh status
```

✅ It should display: SonarQube is running (PID)

2. Create sonar-project.properties

# Go to your Angular project root
```
cd ~/Angular-Calc-App
```

# Create sonar-project.properties file with correct configurations

```
sudo tee sonar-project.properties > /dev/null <<EOF
sonar.projectKey=angular-project
sonar.projectName=Angular Calculator App
sonar.projectVersion=1.0
sonar.sources=src
sonar.language=js
sonar.sourceEncoding=UTF-8
sonar.host.url=http://98.89.32.52:9000
sonar.login=ba4b75f6b96a2a7e9fc75d216c3f2f3c0db1eb7b

```
EOF
Replace sonar.login with your own token if different.

3. Fix File Ownership (Optional but Recommended)

```
sudo chown ubuntu:ubuntu sonar-project.properties

```
SonarQube Analysis


# Run SonarQube analysis from project root

```
cd ~/Angular-Calc-App
sonar-scanner

```

✅ Expected output:


```
INFO: ANALYSIS SUCCESSFUL
INFO: Browse http://98.89.32.52:9000
```
Open the SonarQube dashboard in a browser to view the analysis results.

## IMAGES

** 1.INSTANCE-LAUNCH**

<img width="1360" height="212" alt="instance" src="https://github.com/user-attachments/assets/4b789863-77d9-4c89-9fba-d77420b94a7b" />

**SSH-CONNECT**

<img width="1599" height="625" alt="ssh-connect" src="https://github.com/user-attachments/assets/9a3bcff0-3e2c-4dcb-b5b0-ddfbbdee8cfc" />

**HOSTNAME-CHANGED**

<img width="564" height="128" alt="hostname changed" src="https://github.com/user-attachments/assets/0224ced2-87dc-42de-8dd1-3df05693967a" />

**UPDATE-SERVER**

<img width="905" height="126" alt="update the server" src="https://github.com/user-attachments/assets/871ddba2-5895-4806-be9e-808559a6e572" />

**INSTALL-CURL**

<img width="711" height="170" alt="install curl" src="https://github.com/user-attachments/assets/b13934f0-4d76-453f-98b6-5b69391e00ea" />

**CURL**

<img width="966" height="409" alt="curl " src="https://github.com/user-attachments/assets/65f7b58d-ac81-4dec-a138-c8db07da325c" />

**INSTALL-NODE.JS**

<img width="939" height="317" alt="install node js" src="https://github.com/user-attachments/assets/a6e34033-9ddd-4f2b-abda-c5d3a69feb34" />

**INSTALL-ANGULAR-CLI**

<img width="704" height="251" alt="install angular cli" src="https://github.com/user-attachments/assets/a720cb3b-a0fa-46a5-b703-584920ade5e5" />

**INSTALL-ANGULAR-CLI**

<img width="867" height="503" alt="verify angular cli" src="https://github.com/user-attachments/assets/b3e056dd-eef5-4810-96ed-9c45d90268d5" />

**VERIFY-ANGULAR-CLI**

<img width="867" height="503" alt="verify angular cli" src="https://github.com/user-attachments/assets/6e4c2c11-0d30-4beb-8559-0452136afaa6" />

**GIT-CLONE**
<img width="806" height="221" alt="git clone" src="https://github.com/user-attachments/assets/a2a7e0a3-2567-4303-a2c7-5e1aae5310e8" />

**JAVA-INSTALL**

<img width="931" height="99" alt="8th version java installed" src="https://github.com/user-attachments/assets/3f214860-f867-4314-bfa6-95eb9239cad1" />

**NPM-INSTALL**

<img width="1599" height="578" alt="npm install" src="https://github.com/user-attachments/assets/050177b4-fa43-4824-bcdc-698c882450bc" />

**ACCESS-THE-URL**

<img width="386" height="106" alt="access the URL with4200" src="https://github.com/user-attachments/assets/0d97adfb-1ed1-4d4d-a336-356d0ff8600a" />

**1**

<img width="1550" height="721" alt="accessing" src="https://github.com/user-attachments/assets/cfc4d9ca-2091-4edb-806e-248654928e62" />

**INSTALL-SONAR-SCANNER**

<img width="739" height="119" alt="install sonar scanner" src="https://github.com/user-attachments/assets/1e98ff9f-ead6-4de4-b0bd-15dbcc83bf22" />

**INSTALL-SONAR**

<img width="1599" height="280" alt="install sonar" src="https://github.com/user-attachments/assets/694c5d60-9fe9-4d0f-acc1-c67ba49f17f1" />

**INSTALL-UNZIP**

<img width="1191" height="303" alt="install unzip" src="https://github.com/user-attachments/assets/812436cc-909c-44b7-816b-064921709ef9" />

**EXTRACT-SONAR**

<img width="719" height="175" alt="extract sonar" src="https://github.com/user-attachments/assets/afbf692e-e9b0-4cf3-8989-50cec69e97ca" />

**SONAR-STARTED**

<img width="778" height="175" alt="sonar started" src="https://github.com/user-attachments/assets/2b1f969a-fc91-4bba-91ea-a3586c96d662" />

**ACCESSING-SONAR**

<img width="1599" height="841" alt="sonar opened" src="https://github.com/user-attachments/assets/cada0bb2-4b21-4800-8d07-e2932b86777f" />

**LOGIN-TO-SONAR**


<img width="1472" height="652" alt="loged in to sonar cube" src="https://github.com/user-attachments/assets/09843270-f1ed-453d-b7a0-316bbfa570d7" />

**TOKEN-GENERATED**


<img width="1554" height="713" alt="token generated" src="https://github.com/user-attachments/assets/10cd636e-60ad-47fc-893c-ecd0a25c4d7e" />

**TOKEN-COPIED-IN-PROPERTIES-FILE**


<img width="849" height="840" alt="id copied in file" src="https://github.com/user-attachments/assets/b41a5fe2-20f8-4e16-a72f-8c6ad1c6d711" />

**OUTPUT**


<img width="1526" height="830" alt="output1" src="https://github.com/user-attachments/assets/37f707a9-67ba-4122-a53a-cc8f22272c55" />


**Author**
Pawankumar Kothapalli  
**Environment**: Ubuntu Server   
**Tools Used**: Node.js, Angular, SonarQube 6.7.7, SonarQube Scanner
