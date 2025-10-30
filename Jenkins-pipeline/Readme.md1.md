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
## Screenshots
<img width="1599" height="260" alt="instance" src="https://github.com/user-attachments/assets/19b9e646-bd2e-4fee-8464-fd4183300f7d" />

<img width="752" height="123" alt="hostname-changed" src="https://github.com/user-attachments/assets/4634808d-c70f-4b7d-89d5-94a3a3b3ff04" />


![java](https://github.com/user-attachments/assets/42791cb9-d4aa-45e7-b958-a36d0c4eef4e)



![1](https://github.com/user-attachments/assets/b4a6b96a-6b43-4b2d-bd49-4dfec5992d78)


![2](https://github.com/user-attachments/assets/494f627f-f7c6-4ec8-a5dd-a844fa1d0e0e)


![3](https://github.com/user-attachments/assets/e3d3cbb0-262b-40f9-94f2-b48919c2a36b)


![4](https://github.com/user-attachments/assets/b4441607-7759-4611-94ec-e11d3cc452eb)


![5](https://github.com/user-attachments/assets/fffc75e3-f0ee-465a-887a-adf32e260bfa)


![6](https://github.com/user-attachments/assets/d0fb723c-09d4-4631-b915-e9f27e0f4747)


![7](https://github.com/user-attachments/assets/6121bd5f-df89-4dd7-acec-19ce130a518d)


![8](https://github.com/user-attachments/assets/09c95d5b-18e5-4bfd-8b3a-a35853ff491f)


![9](https://github.com/user-attachments/assets/ef574bdb-2e16-423a-81c6-06445e67b342)


![10](https://github.com/user-attachments/assets/c8446cba-e011-49cc-9519-555cf94a1b53)


![11](https://github.com/user-attachments/assets/5b30233d-2142-4b7e-b951-b763611843cf)



![12](https://github.com/user-attachments/assets/1f9ead32-d5fa-48e8-a59b-c6588a1efaf1)


![13](https://github.com/user-attachments/assets/67ccf284-42fc-4073-be60-acae295e9763)

![14](https://github.com/user-attachments/assets/1bbee640-6e0a-46e7-873b-c2f01ba5cdc1)


![15](https://github.com/user-attachments/assets/0d366bd0-ce7a-4754-8967-7f9686edac09)

![16](https://github.com/user-attachments/assets/5d3a761b-01d2-4fad-8bb0-e059dc1567e0)


![17](https://github.com/user-attachments/assets/ca7dfe9c-ef13-45ac-9586-bd93a92afc08)


![18](https://github.com/user-attachments/assets/ea07cb10-7bad-4a10-bc02-47764c7d2316)


![19](https://github.com/user-attachments/assets/8e3b3e8c-aa6d-47e9-b0c0-72e1fc4152bf)


![20](https://github.com/user-attachments/assets/79dac1e6-3142-42cd-a55c-9fcf9c4d5911)



![21](https://github.com/user-attachments/assets/fa6a509b-64c8-47b6-95cf-f1bff34a03c6)



---

Would you like me to also generate a **PDF** version of this `.md` file for documentation or presentation purposes?
```
