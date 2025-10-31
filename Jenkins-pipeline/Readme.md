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
```
## Screenshots

<img width="1599" height="260" alt="Image" src="https://github.com/user-attachments/assets/36171fbd-a81c-46c9-82db-6c07fb9c841d" />


<img width="752" height="123" alt="Image" src="https://github.com/user-attachments/assets/6b6d07f1-b863-49b8-855c-ce7a4b494a41" />

![Image](https://github.com/user-attachments/assets/3d5c9cf4-7708-49c1-af00-5e772a68f249)


![Image](https://github.com/user-attachments/assets/dd4c0cba-d12c-47e4-96ef-b05f9c2df655)


![Image](https://github.com/user-attachments/assets/5d8b34b8-ad99-4e14-a260-78ffac916db2)


![Image](https://github.com/user-attachments/assets/6ae92878-8452-494b-8016-abebb4c82dee)


![Image](https://github.com/user-attachments/assets/814e00b4-4bcb-4458-8979-2fceaec380e2)


![Image](https://github.com/user-attachments/assets/a92347b7-e13d-48f2-9e0d-6caa59c143b8)


![Image](https://github.com/user-attachments/assets/d051825d-28bc-4b09-8a3f-dbb105befe08)


![Image](https://github.com/user-attachments/assets/a929a41e-bcaa-40ce-bd82-a47c6508b00d)


![Image](https://github.com/user-attachments/assets/f5a9a83e-3b6c-4091-b5db-5406117871e6)


![Image](https://github.com/user-attachments/assets/a12d74dc-1cc4-4575-9163-b5e0f4cb95a6)


![Image](https://github.com/user-attachments/assets/a3bcbbf3-a3c6-4840-987b-434cfca45000)


![Image](https://github.com/user-attachments/assets/62bf5616-2ef7-43f7-97d3-9a4ce447c657)


![Image](https://github.com/user-attachments/assets/32904375-bdfa-4f75-967b-0cf0eb3ba0ea)


![Image](https://github.com/user-attachments/assets/3be475ba-9989-495c-869c-57411512710d)


![Image](https://github.com/user-attachments/assets/a365c6b8-afc3-4040-b3c7-ecd7d77bf55c)


![Image](https://github.com/user-attachments/assets/19286e16-4273-4a86-9852-3f246529928d)


![Image](https://github.com/user-attachments/assets/af3ed6ad-6688-41c0-9148-292270db1c1c)


![Image](https://github.com/user-attachments/assets/680f3816-59a9-49f0-b710-743d4a7ebb2c)


![Image](https://github.com/user-attachments/assets/b5d7eb84-45f4-4958-8555-76407f8f1e9c)


![Image](https://github.com/user-attachments/assets/af0df154-40c7-4982-ae76-b01ce7f8a4cb)


![Image](https://github.com/user-attachments/assets/52da9c43-ad1d-4faf-8cfc-679009dc4ff9)


![Image](https://github.com/user-attachments/assets/4f825b52-0a83-4d3f-b2cd-74d3216c652f)


<img width="1599" height="492" alt="Image" src="https://github.com/user-attachments/assets/6806e820-3ddc-4bc7-a981-7fa534c9c20c" />



---

Would you like me to also generate a **PDF** version of this `.md` file for documentation or presentation purposes?
```
