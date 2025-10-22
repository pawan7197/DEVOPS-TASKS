# Angular Calculator App

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

Notes
Do NOT run the .properties file directly — it is a configuration file.

Always run sonar-scanner from the project root (~/Angular-Calc-App).

Ensure Java 8 is installed and SonarQube server is running.

sonar.sources should point to your actual source folder (src).

sonar.login must be the token, not username/password.

**Author**
Pawankumar Kothapalli  
**Environment**: Ubuntu Server   
**Tools Used**: Node.js, Angular, SonarQube 6.7.7, SonarQube Scanner