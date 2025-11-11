# 🐳 Docker Installation and Basic Commands

## 📘 Overview
This document explains how to install Docker on **Ubuntu Server** and demonstrates the **basic Docker commands** used for managing containers and images.  
The hostname for the server was set as **Docker-Lab**.

---

## 🖥️ Environment Setup

### 🔹 Step 1: Set the Hostname
```
sudo hostnamectl set-hostname docker
```
🔹 Step 2: Reboot the System
```
sudo init 6
```
This command restarts the system to apply the hostname change.

🧱 Docker Installation (Optional Reference)
If Docker is not installed, use the following commands to install it:

```
sudo apt update
```
```
sudo apt install -y ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
  ```
  ```
sudo apt update
```
```
sudo apt install -y docker-ce docker-ce-cli containerd.io
sudo systemctl enable docker
sudo systemctl start docker
docker --version
```

⚙️ Docker Commands Used
🔹 Check Running Containers

```
docker ps
```
🔹 Stop a Container
By name:

```
docker stop nginx
By container ID:
```

```
docker stop d6b80b0fd348
```
🔹 List All Containers (Running + Stopped)

```
docker ps -a
```

🔹 Run a New Container
Run an nginx container in detached mode:


```
docker run -dt nginx
```

🔹 Inspect a Container
View detailed information about a container:

```
docker inspect 6838da896b9b
```

🔹 Start and Stop Containers
Stop:

```
docker stop 6838da896b9b
```

Start:

```
docker start 6838da896b9b
```

🧩 Image Management
🔹 List All Images

```
docker images
```

🔹 Remove an Image
Normal removal:

```
docker rmi d261fd19cb63
```

Force removal:

```
docker rmi -f d261fd19cb63
```

🗑️ Container Cleanup
🔹 Remove a Container

```
docker rm -f 6838da896b9b
```

📋 Final Verification
Check active containers and available images:

```
docker ps
docker images
```