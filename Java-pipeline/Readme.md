## End-to-End CI/CD Pipeline for Java Web Application
## Java 17 | Maven | SonarQube | Nexus Repository | Tomcat | Jenkins:

 ## Multi-Server Architecture:

## CI/CD Architecture:

(Illustrative diagram – replace with your own if available)
This project demonstrates a fully automated, multi-server CI/CD pipeline for a Java web application (Java-Web-Calculator-App) using Jenkins as the orchestration engine. The pipeline includes source code analysis, secure artifact management, and zero-downtime deployment to a remote Tomcat server.

## 📁 Project Overview:

Source Code: mrtechreddy/Java-Web-Calculator-App Build Tool: Apache Maven (3.9.11) Language: Java 17 CI/CD Engine: Jenkins (Distributed across 4 EC2 instances) Quality Gate: SonarQube (Code Quality & Security) Artifact Storage: Sonatype Nexus Repository Deployment Target: Apache Tomcat (Remote)

## 🧱 Architecture:
```
SVG content

Server Roles

Jenkins

CI/CD Orchestrator

jenkins

SonarQube
Static Code Analysis

sonar

Nexus
Binary Artifact Repository

nexus

Tomcat
Application Runtime
tomcat
```
 
## ⚙️ Prerequisites:

4 AWS EC2 instances (Ubuntu 22.04 LTS recommended) Network connectivity between all servers (private IPs preferred) GitHub account with a personal access token (classic, with repo scope) DNS or /etc/hosts entries for inter-server resolution (optional but recommended) 🔧 Setup Guide

## 1. Configure Hostnames:

**On each server, run:**

**On Jenkins server:**
```
sudo hostnamectl set-hostname jenkins
 ```

**On SonarQube server:**
```
sudo hostnamectl set-hostname sonar
 ```

**On Nexus server:**
```
sudo hostnamectl set-hostname nexus
 ```

**On Tomcat server:**
```
sudo hostnamectl set-hostname tomcat
 ```

**sudo reboot:**

## 2. Install Java 17 & Maven (All Servers):
```
sudo apt update -y
sudo apt install openjdk-17-jdk maven -y
 
java -version   # Should show openjdk version "17.x"
mvn -version    # Should show Apache Maven 3.9.11+
 ```

## 3. Setup Jenkins Working Directory:
```
mkdir -p /home/ubuntu/jenkins
 ```

## 4. Configure SSH Key-Based Authentication (From Jenkins):

**On the Jenkins server, generate and distribute SSH keys:**
```
ssh-keygen 
```

 
**Replace IPs with your actual private IPs:**
```
ssh-copy-id ubuntu@<SONAR_IP>
ssh-copy-id ubuntu@<NEXUS_IP>
ssh-copy-id ubuntu@<TOMCAT_IP>
```

 
## ✅ Test: ssh ubuntu@<SONAR_IP> → should log in without password:

## 5. Install Jenkins Plugins:

**In Jenkins UI**
```
(http://<JENKINS_IP>:8080):
```

``` 
Manage Jenkins → Plugins → Available:
```
**Install:**
```
Publish Over SSH
GitHub Integration
Nexus Artifact Uploader
SonarQube Scanner
Sonar Quality Gates
SSH Agent Plugin
SSH Build Agents
```

 
**💡 Restart Jenkins after installation:**


## 6. Configure Jenkins Credentials:
```
Go to: Manage Jenkins → Credentials → Global
```

 
**Add the following:**
```
github-token:

Secret text

Your GitHub Personal Access Token

nexus:

Username & Password

Nexus admin credentials

tomcat:

Username & Password Tomcat Manager user (see tomcat-users.xml )

SSH Key:

SSH Username with Private Key Username: ubuntu , Private Key: Paste ~/.ssh/id_rsa
```
## 7. Add Jenkins Agent Nodes:
```
Manage Jenkins → Nodes → New Node
```

 
## Create three permanent agents:
```
Name: sonar, nexus, tomcat
Remote root directory: /home/ubuntu/jenkins
Launch method: Launch agents via SSH
Host: Private IP or hostname
Credentials: Select the SSH key 
```

 
## ✅ Ensure all nodes show Connected status:

📜 Jenkins Pipeline (Jenkinsfile)

## The pipeline is declarative and runs across multiple agents:

```groovy
pipeline {
    agent { label 'sonar' }
    tools {
        jdk 'JDK17'
        maven 'Maven'
    }
    environment {
        SONARQUBE_SERVER = 'http://18.212.142.140:9000'
        SONARQUBE_TOKEN = 'squ_aa5e62c5e4b239d040227e37930671ede97fb85b'
        MVN_SETTINGS = '/etc/maven/settings.xml'
        NEXUS_URL = 'http://18.208.136.157:8081'
        NEXUS_REPO = 'maven-releases'
        NEXUS_GROUP = 'com.web.cal'
        NEXUS_ARTIFACT = 'webapp-add'
        TOMCAT_URL = 'http://54.83.80.22:8080/manager/text'
    }
    stages {
        /* === Stage 1: Checkout Code === */
        stage('Checkout Code') {
            steps {
                echo '📦 Cloning source from GitHub...'
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/main']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/mrtechreddy/Java-Web-Calculator-App.git'
                    ]]
                ])
            }
        }
        /* === Stage 2: SonarQube Analysis === */
        stage('SonarQube Analysis') {
            steps {
                echo '🔍 Running SonarQube static analysis...'
                sh '''
                mvn clean verify sonar:sonar \
                  -DskipTests \
                  -Dsonar.host.url=${SONARQUBE_SERVER} \
                  -Dsonar.login=${SONARQUBE_TOKEN} \
                  --settings ${MVN_SETTINGS}
                '''
            }
        }
        /* === Stage 3: Build Artifact === */
        stage('Build Artifact') {
            steps {
                echo '⚙️ Building WAR...'
                sh 'mvn clean package -DskipTests --settings ${MVN_SETTINGS}'
                sh 'echo ✅ Build Completed!'
                sh 'ls -lh target/*.war || echo "No WAR file found."'
            }
        }
        /* === Stage 4: Upload Artifact to Nexus === */
        stage('Upload Artifact to Nexus') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'nexus', usernameVariable: 'NEXUS_USR', passwordVariable: 'NEXUS_PSW')]) {
                    sh '''#!/bin/bash
                    set -e
                    WAR_FILE=$(find target -type f -name "*.war" | head -n1)
                    if [[ ! -f "$WAR_FILE" ]]; then
                        echo "❌ No WAR file found in target/"; exit 1
                    fi
                    FILE_NAME=$(basename "$WAR_FILE")
                    VERSION="0.0.${BUILD_NUMBER}"
                    GROUP_PATH=$(echo "${NEXUS_GROUP}" | tr '.' '/')
                    echo "📤 Uploading $FILE_NAME to Nexus as version $VERSION..."
                    curl -f -u "${NEXUS_USR}:${NEXUS_PSW}" --upload-file "$WAR_FILE" \
                    "${NEXUS_URL}/repository/${NEXUS_REPO}/${GROUP_PATH}/${NEXUS_ARTIFACT}/${VERSION}/${NEXUS_ARTIFACT}-${VERSION}.war"
                    echo "✅ Artifact uploaded successfully to Nexus!"
                    '''
                }
            }
        }
        /* === Stage 5: Deploy to Tomcat === */
        stage('Deploy to Tomcat') {
            agent { label 'tomcat' }
            steps {
                withCredentials([
                    usernamePassword(credentialsId: 'nexus', usernameVariable: 'NEXUS_USR', passwordVariable: 'NEXUS_PSW'),
                    usernamePassword(credentialsId: 'tomcat', usernameVariable: 'TOMCAT_USR', passwordVariable: 'TOMCAT_PSW')
                ]) {
                    sh '''#!/bin/bash
                    set -e
                    cd /tmp || exit 1
                    rm -f *.war
                    VERSION="0.0.${BUILD_NUMBER}"
                    GROUP_PATH=$(echo "${NEXUS_GROUP}" | tr '.' '/')
                    WAR_URL="${NEXUS_URL}/repository/${NEXUS_REPO}/${GROUP_PATH}/${NEXUS_ARTIFACT}/${VERSION}/${NEXUS_ARTIFACT}-${VERSION}.war"
                    echo "⬇️ Downloading WAR from Nexus: $WAR_URL"
                    curl -u "${NEXUS_USR}:${NEXUS_PSW}" -O "$WAR_URL"
                    WAR_FILE=$(basename "$WAR_URL")
                    APP_NAME="${NEXUS_ARTIFACT}"
                    echo "🧹 Undeploying old app (if exists)..."
                    curl -u "${TOMCAT_USR}:${TOMCAT_PSW}" "${TOMCAT_URL}/undeploy?path=/${APP_NAME}" || true
                    echo "🚀 Deploying new WAR to Tomcat..."
                    curl -u "${TOMCAT_USR}:${TOMCAT_PSW}" --upload-file "$WAR_FILE" \
                    "${TOMCAT_URL}/deploy?path=/${APP_NAME}&update=true"
                    echo "✅ Deployment successful! Application updated."
                    '''
                }
            }
        }
    }
    post {
        success {
            echo '🎉 Pipeline completed successfully — Application live on Tomcat!'
        }
        failure {
            echo '❌ Pipeline failed — Check Jenkins logs.'
        }
    }
}
```

 
## ✅ Note: Replace <SONAR_IP>, <NEXUS_IP>, <TOMCAT_IP> with actual private IPs:

## 🔄 Pipeline Stages Explained:

**1. Checkout Code:**

Clones
main
branch from GitHub

 
**2. SonarQube Analysis:**

Runs static code analysis (skips tests)

**3. Build Artifact:**

Packages .war file using Maven

**4. Upload to Nexus:**

Uploads versioned WAR to Nexus repo ( 0.0.${BUILD_NUMBER} )

**5. Deploy to Tomcat:**

Downloads WAR from Nexus and deploys via Tomcat Manager API

## 🔐 Security Notes:

Never hardcode secrets in Jenkinsfile – always use withCredentials Use private IPs for inter-server communication (not public IPs) Restrict Nexus/Tomcat access via security groups Rotate SonarQube token and GitHub PAT periodically

## 🛠️ Required Configurations Tomcat (tomcat-users.xml)
```
<tomcat-users>
  <role rolename="manager-script"/>
  <user username="admin" password="secure_password" roles="manager-script"/>
</tomcat-users>
```
## Maven settings.xml (for Nexus):

 
**Place in /etc/maven/settings.xml on all servers:**
```
<servers>
  <server>
    <id>nexus</id>
    <username>admin</username>
    <password>your-nexus-password</password>
  </server>
</servers>
```

 `
## ✅ Verification Checklist:

**Java 17:**
```
java -version
```

**Maven:**
```
mvn -version
```

**Jenkins Nodes:**


Green "Connected" status

**SonarQube:**
 
 
**Access:**
```
http://<SONAR_IP>:9000
```
 
**Nexus:**

**Access:**
```
http://<NEXUS_IP>:8081
```

 
**Tomcat Manager:**
```
curl -u admin:pass http://<TOMCAT_IP>:8080/manager/text/list
```

## IMAGES
**1**
<img width="1580" height="494" alt="1" src="https://github.com/user-attachments/assets/b389476d-cfdb-4e64-ad21-4694fa6ccf96" />
**2**
<img width="1599" height="136" alt="8" src="https://github.com/user-attachments/assets/03c6a605-62d8-4ccd-ae6a-1363440c7c26" />
**3**
<img width="1599" height="136" alt="8" src="https://github.com/user-attachments/assets/0d57dca9-1034-438a-9934-25caab24fa65" />
**4**
<img width="1336" height="725" alt="10" src="https://github.com/user-attachments/assets/a19c5f12-778d-468d-9ace-42276befdd69" />
**5**
<img width="1403" height="735" alt="11" src="https://github.com/user-attachments/assets/46cd2fe2-1807-46a7-9215-1b854f6eb028" />
**6**
<img width="1515" height="849" alt="12" src="https://github.com/user-attachments/assets/c4603f5b-6054-4207-b757-b3df1bd73909" />
**7**
<img width="708" height="105" alt="13-nexus" src="https://github.com/user-attachments/assets/8437a03f-fd1f-4f2e-a328-752a242ee904" />
**8**
<img width="1570" height="296" alt="14" src="https://github.com/user-attachments/assets/e10d3824-c510-42fa-a441-41cb486042fa" />
**9**
<img width="1589" height="538" alt="15" src="https://github.com/user-attachments/assets/fbf0edb2-e55c-4f09-b68f-34918cd06914" />
**10**
<img width="1589" height="561" alt="16" src="https://github.com/user-attachments/assets/18519ab1-785b-49f0-8836-668f9d8aee51" />
**11**
<img width="1599" height="251" alt="17" src="https://github.com/user-attachments/assets/ce93be0b-3d12-43f9-9a4a-91804ed56eb6" />
**12**
<img width="1485" height="102" alt="18" src="https://github.com/user-attachments/assets/e23c9b66-fdcb-4935-a567-85f48d8d4088" />
**13**
<img width="1599" height="464" alt="19" src="https://github.com/user-attachments/assets/7bc1d225-d7e7-41aa-a9ec-8dff64acb971" />
**14**
<img width="1599" height="522" alt="20" src="https://github.com/user-attachments/assets/26a429a1-d225-4b95-b65e-4f673767d490" />
**15**
<img width="1599" height="722" alt="21" src="https://github.com/user-attachments/assets/d440eaa3-08e5-48c1-a03c-30cfcdee0f65" />
**16**
<img width="1599" height="178" alt="22" src="https://github.com/user-attachments/assets/8c8dbd74-ebfb-4264-ae29-4d9eb36bcb4b" />
**17**
<img width="1593" height="446" alt="23" src="https://github.com/user-attachments/assets/258adf5b-65c0-485d-9273-c6e1738aa7f4" />

**18**
<img width="1597" height="675" alt="24" src="https://github.com/user-attachments/assets/70cc6865-e8e4-4f3a-8720-ebf853df1c9c" />
**19**
<img width="1599" height="396" alt="25" src="https://github.com/user-attachments/assets/a2995e52-cd77-4cee-80f0-cd217607b26b" />
**20**
<img width="1599" height="416" alt="26" src="https://github.com/user-attachments/assets/2370d60b-877a-41eb-9567-220833cfb0a3" />
**21**
<img width="1597" height="687" alt="27" src="https://github.com/user-attachments/assets/a6cbecfc-9f5b-4064-b358-58dc24da1600" />
**22**
<img width="1510" height="258" alt="28" src="https://github.com/user-attachments/assets/474882e2-14b3-44c5-8413-51799be0397a" />
**23**
<img width="1599" height="738" alt="29" src="https://github.com/user-attachments/assets/6d3038b9-eb36-423b-84ac-424764a6c17d" />
**24**
<img width="1599" height="193" alt="30" src="https://github.com/user-attachments/assets/de285f02-c351-4c0e-a4ea-ae29017befa0" />
**25**
<img width="1599" height="833" alt="31" src="https://github.com/user-attachments/assets/eaef8687-887c-4a28-ad9f-117fff2deae1" />
**26**
<img width="1599" height="440" alt="32" src="https://github.com/user-attachments/assets/d7fbf4e7-88f5-4c40-9ca3-c927f2dd4c7a" />
**27**
<img width="1599" height="834" alt="33" src="https://github.com/user-attachments/assets/7a008cc8-db2b-4124-af45-514059ef5fed" />
**28**
<img width="1599" height="166" alt="34" src="https://github.com/user-attachments/assets/744ec966-2940-4ff8-8e70-a02fe29b8f19" />
**29**
<img width="1420" height="458" alt="35" src="https://github.com/user-attachments/assets/57b81d01-eaed-4879-8387-29bb56923b41" />

**30**
<img width="1599" height="393" alt="36-sonar" src="https://github.com/user-attachments/assets/8087d413-2487-486a-9827-7c1c49b96e36" />
**31**

<img width="1580" height="387" alt="37" src="https://github.com/user-attachments/assets/47cdd133-d36e-42e3-80a9-60a15ad8379c" />
**32**
<img width="1599" height="576" alt="38" src="https://github.com/user-attachments/assets/1db76aff-87e8-4dd1-a455-235a6292c2c4" />
**33**
<img width="1599" height="573" alt="39" src="https://github.com/user-attachments/assets/ce017085-35e4-420d-8698-28a843e6fad5" />
**34**
<img width="1599" height="828" alt="40" src="https://github.com/user-attachments/assets/d22ee467-043f-4be9-8f34-02a97b814156" />
**35**
<img width="1599" height="643" alt="41" src="https://github.com/user-attachments/assets/343bad80-388b-497d-a80c-ac3cca9056b3" />
**36**
<img width="954" height="157" alt="42" src="https://github.com/user-attachments/assets/9183aa16-d513-440e-8aed-75a7364682a5" />
**37**
<img width="1250" height="162" alt="43" src="https://github.com/user-attachments/assets/66cab8ff-ff8d-4c34-99a7-f5c8b0d64925" />
**38**
<img width="999" height="167" alt="44" src="https://github.com/user-attachments/assets/36fe0815-fcfa-4c35-b85e-7d711ef3aa9a" />
**39**
<img width="1599" height="393" alt="45" src="https://github.com/user-attachments/assets/1a93774b-2fed-4dbb-88af-f61416652c25" />
**40**
<img width="891" height="172" alt="46" src="https://github.com/user-attachments/assets/2539250a-8f72-4476-9388-c944b1ab6221" />
**41**
<img width="1599" height="877" alt="47" src="https://github.com/user-attachments/assets/bbb947bc-dc7e-44a7-898b-727fe25837bd" />
**42**
<img width="1495" height="179" alt="48" src="https://github.com/user-attachments/assets/556d9cf9-e27e-41e6-9ee1-435bcda6f42e" />
**43**
<img width="1589" height="856" alt="49" src="https://github.com/user-attachments/assets/aedd5672-0e16-41b6-8cd2-3df2d62bf735" />
**44**
<img width="1599" height="206" alt="50" src="https://github.com/user-attachments/assets/2bf2f7cc-8878-4cc3-aac0-f915af3eda69" />
**45**
<img width="1599" height="826" alt="51" src="https://github.com/user-attachments/assets/f4c14427-0b49-4a4d-bf39-1df43e3ddefe" />
**46**
<img width="1599" height="227" alt="52" src="https://github.com/user-attachments/assets/8fd7f3da-7236-43d2-9c7d-4aaefc4d666a" />
**47**
<img width="1472" height="162" alt="53" src="https://github.com/user-attachments/assets/409c3238-91ad-43e7-a30f-f2d983aeec7f" />
**48**
<img width="1555" height="761" alt="54" src="https://github.com/user-attachments/assets/8441b257-d7cc-4b44-ac6b-6a476d854cc9" />
**49**
<img width="1174" height="701" alt="55" src="https://github.com/user-attachments/assets/da127a96-ff30-4e96-b3d9-8005bf2b859b" />
**50**
<img width="1599" height="757" alt="56" src="https://github.com/user-attachments/assets/6159c59d-97e2-4507-b69f-6a0d619e4027" />
**51**
<img width="1599" height="497" alt="57" src="https://github.com/user-attachments/assets/39cdf4bb-eacc-4874-8ec3-075c7f5d3fc1" />
**52**
<img width="1599" height="599" alt="58" src="https://github.com/user-attachments/assets/b0456927-96b7-4a23-a433-4b1c5d15dc43" />
**53**
<img width="1581" height="272" alt="59" src="https://github.com/user-attachments/assets/935cdd64-75fb-49a2-ad56-50dbf3553681" />
**54**
<img width="1562" height="687" alt="1 1" src="https://github.com/user-attachments/assets/e7b3f16c-f90f-4a57-a823-1db5621636e1" />
**55**
<img width="1578" height="790" alt="2" src="https://github.com/user-attachments/assets/aa72987e-1b44-46e4-82f7-c93aab27b162" />
**56**
<img width="1599" height="776" alt="3" src="https://github.com/user-attachments/assets/0f16ffd1-bc16-40fb-89e8-5afd8f41d476" />
**57**
<img width="1598" height="847" alt="4" src="https://github.com/user-attachments/assets/f4ab3b13-fcee-4cd4-8fe0-95c5eb90fe8c" />
**58**
<img width="1598" height="796" alt="5" src="https://github.com/user-attachments/assets/0a84ee5a-be71-43f1-ab35-9d08d3c04675" />
**59**
<img width="1586" height="794" alt="6" src="https://github.com/user-attachments/assets/a4300826-fb41-475b-8c38-af5fe02570c5" />
**60**
<img width="1029" height="650" alt="7" src="https://github.com/user-attachments/assets/f50456c7-762c-4ea3-85d1-8f61db91c7c6" />
 
## 🎯 Final Outcome:

✅ Code pushed to GitHub triggers Jenkins pipeline

✅ Code quality enforced via SonarQube

✅ Artifact securely stored in Nexus with versioning

✅ Application auto-deployed to Tomcat

✅ Full traceability from commit → build → deploy

**Author**: *Pawan Kumar Kothapalli*

**Devops-Engineer**

**Mail-Id**: pawankumarkothapalli22644@gmail.com

**Linkedin-URL**: https://www.linkedin.com/in/pawan-kumar-kothapalli-17865b302/


 
