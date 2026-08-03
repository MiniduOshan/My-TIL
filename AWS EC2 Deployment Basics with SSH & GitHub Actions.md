# TIL - AWS EC2 Deployment with SSH & GitHub Actions

**Date:** 2026-08-03

## Overview

Today I learned how to:

- Connect to an AWS EC2 instance using an SSH private key.
- Install the required dependencies on the server.
- Clone and deploy a GitHub repository.
- Automate deployments using GitHub Actions.
- Secure deployment credentials using GitHub Secrets.

---

# 1. Connecting to an EC2 Instance via SSH

### Step 1: Change the Private Key Permission

Before connecting, make sure the private key has the correct permissions.

```bash
chmod 400 my-key.pem
```

---

### Step 2: Connect to the Server

For Ubuntu instances:

```bash
ssh -i my-key.pem ubuntu@<EC2_PUBLIC_IP>
```

Example:

```bash
ssh -i my-key.pem ubuntu@54.xxx.xxx.xxx
```

For Amazon Linux:

```bash
ssh -i my-key.pem ec2-user@<EC2_PUBLIC_IP>
```

---

# 2. Update the Server

```bash
sudo apt update
sudo apt upgrade -y
```

---

# 3. Install Git

```bash
sudo apt install git -y
```

Verify the installation:

```bash
git --version
```

---

# 4. Install Docker

```bash
sudo apt install docker.io -y
```

Start Docker:

```bash
sudo systemctl start docker
```

Enable Docker to start automatically:

```bash
sudo systemctl enable docker
```

Allow the current user to run Docker commands without sudo:

```bash
sudo usermod -aG docker $USER
```

Reconnect to the server after running the above command.

Verify Docker:

```bash
docker --version
```

---

# 5. Install Docker Compose

Check whether Docker Compose is already installed.

```bash
docker compose version
```

If not installed:

```bash
sudo apt install docker-compose-plugin -y
```

---

# 6. Clone Your GitHub Repository

```bash
git clone https://github.com/username/project.git
```

Navigate into the project directory.

```bash
cd project
```

---

# 7. Build and Run the Application

```bash
docker compose up -d --build
```

Check running containers:

```bash
docker ps
```

---

# 8. GitHub Actions Deployment Workflow

Deployment flow:

```
Developer
   │
   ▼
Push Code
   │
   ▼
GitHub Repository
   │
   ▼
GitHub Actions
   │
   ▼
SSH into EC2
   │
   ▼
Pull Latest Code
   │
   ▼
Docker Compose Build
   │
   ▼
Application Updated
```

---

# 9. Required GitHub Secrets

Navigate to:

**Repository → Settings → Secrets and Variables → Actions**

Add the following secrets:

| Secret | Description |
|---------|-------------|
| EC2_HOST | Public IP of the EC2 instance |
| EC2_USERNAME | ubuntu or ec2-user |
| EC2_SSH_KEY | Contents of the private `.pem` file |
| PORT *(optional)* | SSH port (default: 22) |

> Never upload your `.pem` file directly to GitHub.

---

# 10. Example GitHub Actions Workflow

```yaml
name: Deploy to EC2

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v4

      - name: Deploy to EC2
        uses: appleboy/ssh-action@v1.2.0
        with:
          host: ${{ secrets.EC2_HOST }}
          username: ${{ secrets.EC2_USERNAME }}
          key: ${{ secrets.EC2_SSH_KEY }}
          script: |
            cd /home/ubuntu/project
            git pull origin main
            docker compose down
            docker compose up -d --build
```

---

# 11. Security Best Practices

- Never commit your private SSH key to GitHub.
- Store secrets in GitHub Secrets.
- Use IAM users instead of the AWS root account.
- Restrict SSH access with Security Groups.
- Keep the server updated regularly.
- Rotate SSH keys if they are ever compromised.

---

# Common Commands

```bash
# Connect to EC2
ssh -i my-key.pem ubuntu@<EC2_PUBLIC_IP>

# Update packages
sudo apt update

# Install Git
sudo apt install git -y

# Install Docker
sudo apt install docker.io -y

# Enable Docker
sudo systemctl enable docker

# Start Docker
sudo systemctl start docker

# Clone repository
git clone <repository-url>

# Build and run containers
docker compose up -d --build

# View running containers
docker ps
```

---

# Summary

Today I learned how to deploy applications on AWS EC2 using SSH authentication, prepare the server by installing Git and Docker, deploy applications with Docker Compose, and automate deployments using GitHub Actions with secure secret management.
