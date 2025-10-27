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
## 🖥️ Step 2: Set the Hostname
Rename the instance for easier identification and reboot to apply the change:

```
sudo hostnamectl set-hostname Jenkins-Lab
sudo init 6
```
After reboot, reconnect using SSH.

## ⚙️ Step 3: Update Packages and Install Java

```
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
java -version
```

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

## ▶️ Step 5: Start and Enable Jenkins

```
sudo systemctl enable jenkins
sudo systemctl start jenkins
sudo systemctl status jenkins
```

## 🌐 Step 6: Access Jenkins
In your browser, open:

```
http://<your-ec2-public-ip>:8080
```

## Retrieve the Jenkins administrator password:

```
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

**Copy the password and paste it into the Jenkins setup wizard**

## ✅ Step 7: Complete the Initial Setup

Choose Install suggested plugins

Wait for the plugin installation to complete

Create your first admin user (next step)

Confirm the Jenkins URL and finish setup

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

## 🛠️ Step 9: Create Your First Jenkins Project (Freestyle Job)
* From the dashboard, click New Item

* Enter a project name (e.g., My-First-Project)

* Choose Freestyle project and click OK

* Click Save

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