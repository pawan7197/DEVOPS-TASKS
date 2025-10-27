# 🚀 Jenkins Installation on AWS EC2 (t2.micro)

This guide provides a **step-by-step walkthrough** to install and configure Jenkins on an **AWS EC2 t2.micro instance** running **Ubuntu**.  
It also includes steps on how to create your **first Jenkins user and project**.

---

## 🧰 Prerequisites

Before you begin, ensure you have:

- An AWS EC2 instance (t2.micro or larger) running Ubuntu  
- SSH access to the instance  
- `sudo` privileges  
- Port **8080** open in the **Security Group** (for Jenkins web access)

---

## 🖥️ Step 1: Connect to Your EC2 Instance

```
ssh -i your-key.pem ubuntu@<your-ec2-public-ip>
```
<img width="1365" height="190" alt="instance" src="https://github.com/user-attachments/assets/127a7ec3-f0a2-4858-9c31-297b96ed2c25" />

<img width="1372" height="533" alt="port 8080" src="https://github.com/user-attachments/assets/45a5679c-9900-430c-a552-7a1a75d7baa5" />

<img width="1299" height="201" alt="SSH-connect" src="https://github.com/user-attachments/assets/88cdf808-a68e-4aae-91e7-1acd8108cb95" />


## 🖥️ Step 2: Set the Hostname
Rename the instance for easier identification and reboot to apply the change:

```
sudo hostnamectl set-hostname Jenkins-Lab
sudo init 6
```

<img width="660" height="73" alt="change-hostname" src="https://github.com/user-attachments/assets/3aadda8d-24f8-4dc5-ae35-4273a65d7962" />


After reboot, reconnect using SSH.

## ⚙️ Step 3: Update Packages and Install Java

```
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
java -version
```
<img width="1313" height="175" alt="Install-Java" src="https://github.com/user-attachments/assets/2f28854a-e6bf-4ee8-b10f-a69984414410" />

<img width="954" height="140" alt="java-version" src="https://github.com/user-attachments/assets/88d27a30-66e2-4f50-a3a9-effbf95656c7" />

Run java -version to verify successful installation.

## 🧩 Step 4: Install Jenkins
Add the Jenkins repository, import its GPG key, and install Jenkins:

```
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y
```

<img width="1599" height="474" alt="install-Jenkins from website" src="https://github.com/user-attachments/assets/8d8c7d8c-0664-4e3b-9449-39c3fd0e3d03" />

<img width="1119" height="273" alt="Jenkins-install" src="https://github.com/user-attachments/assets/fc324959-7bef-467b-b577-f79054d7180e" />


## ▶️ Step 5: Start and Enable Jenkins

```
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

<img width="715" height="196" alt="start enable-Jenkins" src="https://github.com/user-attachments/assets/ca744377-0b3c-4d3e-b3ad-c4c5861f9fb4" />

<img width="1599" height="553" alt="Jenkins-started" src="https://github.com/user-attachments/assets/b02b609b-8906-4351-9b00-ac9e17e3eb01" />


## 🌐 Step 6: Access Jenkins
In your browser, open:

```
http://<your-ec2-public-ip>:8080
```
<img width="1345" height="421" alt="access-jenkins" src="https://github.com/user-attachments/assets/c42d7689-ed39-4ede-935b-3c1501219745" />

<img width="1203" height="118" alt="public-ip-address" src="https://github.com/user-attachments/assets/2cdf4920-6a34-4e6c-b466-1b336b312401" />

<img width="1523" height="772" alt="Jenkins-opened" src="https://github.com/user-attachments/assets/08454b2b-fbd1-46d6-8c01-c08ac5349f89" />



## Retrieve the Jenkins administrator password:

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

<img width="711" height="221" alt="to-know-the-password" src="https://github.com/user-attachments/assets/36eca190-9ba9-49ba-95a1-f37b43fcfd43" />

<img width="905" height="74" alt="password-opened" src="https://github.com/user-attachments/assets/78e2fd34-1a80-43d2-997c-ccfbc3c60b7d" />

<img width="918" height="219" alt="password-copied" src="https://github.com/user-attachments/assets/44d56fd7-335d-462d-babf-6bb2a6b3584c" />

**Copy the password and paste it into the Jenkins setup wizard**

## ✅ Step 7: Complete the Initial Setup

## Choose Install suggested plugins
<img width="1079" height="755" alt="suggested-plugins-started" src="https://github.com/user-attachments/assets/5645d2c5-2fee-4853-abaf-3b3d1d257af3" />

<img width="1372" height="796" alt="create-user" src="https://github.com/user-attachments/assets/0571ea1f-8d9c-48be-89b0-e6a7fc55f1f0" />


## Wait for the plugin installation to complete

<img width="1317" height="758" alt="Jenkins-URL-generated" src="https://github.com/user-attachments/assets/e277ab8c-4310-41e9-8556-35c9ca2f20f7" />

Create your first admin user (next step)

## Confirm the Jenkins URL and finish setup
<img width="1317" height="758" alt="Jenkins-URL-generated" src="https://github.com/user-attachments/assets/5315b410-73c0-4cd5-acfb-809d31cea204" />

<img width="512" height="289" alt="Jenkins-ready" src="https://github.com/user-attachments/assets/a06b129d-307a-4d8c-9a48-1521828c8ef8" />


## 👤 Step 8: Create a Jenkins User (Admin Account)

When prompted, enter your details:

* Username: admin

* Password: your secure password

* Full name: (optional)

* Email address: (optional)

* Click Save and Continue.
Confirm the Jenkins URL and click Save and Finish.

* To create more users later:
Manage Jenkins → Users → Create User

<img width="1599" height="762" alt="Manage-Jenkins" src="https://github.com/user-attachments/assets/b786a48f-7a58-41f0-995a-9aea1c003297" />

<img width="1587" height="411" alt="Go-to-users" src="https://github.com/user-attachments/assets/80819443-10bf-4804-b056-3e75bb157687" />

<img width="1534" height="719" alt="create-users" src="https://github.com/user-attachments/assets/d06b6fae-1893-4ed5-ae79-fde1114d833a" />

<img width="1515" height="645" alt="user-creation" src="https://github.com/user-attachments/assets/c9bc5c05-f939-4017-8109-1716b7584251" />


## 🛠️ Step 9: Create Your First Jenkins Project (Freestyle Job)
* From the dashboard, click New Item

<img width="1296" height="730" alt="ceating-my-first-project" src="https://github.com/user-attachments/assets/31cce65b-1c80-4c88-ba47-1eb915085088" />

* Enter a project name (e.g., My-First-Project)

* Choose Freestyle project and click OK

* Click Save

  <img width="1557" height="757" alt="save" src="https://github.com/user-attachments/assets/66c95b02-f55d-4230-9fef-c2b9be38fcf7" />

<img width="1593" height="570" alt="saved" src="https://github.com/user-attachments/assets/0ab1b809-a6c9-4b3c-b8d6-c079b57571f0" />

<img width="1599" height="486" alt="dashboard" src="https://github.com/user-attachments/assets/52108e18-ac45-4c11-9094-eead50aadbd6" />


To run the job → click Build Now

View output → click build number under Build History

## 🧾 Notes
* Instance Type: t2.micro

* Default Jenkins Port: 8080

Service Commands
Action	Command
## Start Jenkins	**sudo systemctl start jenkins**
## Stop Jenkins	**sudo systemctl stop jenkins**
## Restart Jenkins **sudo systemctl restart jenkins**
## Check Status	**sudo systemctl status jenkins**

⚠️ Ensure your EC2 Security Group allows inbound traffic on port 8080 to access Jenkins web interface

## Author:
**Pawan Kumar Kothapalli**
**Devops-Engineer**
**Mail-Id**: pawankumarkothapalli22644@gmail.com
**Linkedin-URL**: https://www.linkedin.com/in/pawan-kumar-kothapalli-17865b302/
