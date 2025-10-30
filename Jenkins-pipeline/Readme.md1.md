Sure — here’s your complete **Markdown (.md)** file content:

---

````markdown
# CI/CD Pipeline Using Jenkins and GitHub Webhooks

## Overview
This project demonstrates a complete **CI/CD pipeline** built using **Jenkins**.  
The pipeline automates the process of cloning source code, testing it, building it into deployable artifacts, and finally deploying it to the target environment.

---

## Source Code Repository
This pipeline uses the following GitHub repository as the source:

**Repository:** [Java Web Calculator App] (https://github.com/pawan7197/Java-Web-Calculator-App.git)

---

## Pipeline Stages

### 1. Cloning Job
- Fetches the latest code from GitHub.

### 2. Test Job
- Executes automated tests to verify the integrity and functionality of the code.

### 3. Build Job
- Builds the project and creates the output artifacts.

### 4. Deploy Job
- Deploys the final build to the target server/environment.

---

## Server Details
- **Jenkins Server:** AWS EC2 Instance (t2.micro)

---

## Jenkins Installation Script

The following script was used to install Jenkins on an Ubuntu server:

```bash
#!/bin/bash
sudo apt update
sudo apt install fontconfig openjdk-21-jre -y
sudo wget -O /etc/apt/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/etc/apt/keyrings/jenkins-keyring.asc]" \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null

sudo apt update
sudo apt install jenkins -y

echo "--------------------------- Jenkins has been installed ------------------------"
````

---

## Jenkins Setup Steps

1. Installed Jenkins using a `script.sh` file.
2. Accessed Jenkins via **http://<server-ip>:8080**.
3. Retrieved Jenkins initial admin password from the system path.
4. Created admin credentials for Jenkins dashboard usage.
5. Created the four jobs listed above.
6. Installed the following plugins:

   * Build Pipeline Plugin
   * GitHub Plugin
   * GitHub Webhook Plugin
7. Configured pipeline view to visualize and trigger jobs sequentially.

---

## GitHub Webhook Integration

* Configured a webhook in GitHub to notify Jenkins upon every code push.
* Jenkins automatically triggered the pipeline when changes were pushed.

---

## Pipeline Flow

```
GitHub Commit → Clone Job → Test Job → Build Job → Deploy Job
```

---

## Conclusion

This CI/CD setup ensures **automated, repeatable, and reliable software delivery** triggered directly from source code changes.
It helps maintain consistency, reduces manual interventions, and increases deployment efficiency.

```

---

Would you like me to also generate a **PDF** version of this `.md` file for documentation or presentation purposes?
```
