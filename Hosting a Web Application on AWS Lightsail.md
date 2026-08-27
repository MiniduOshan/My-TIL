# TIL: Hosting a Web Application on AWS Lightsail

📅 Date: 2026-08-28

Today I learned how to deploy and host a web application on **AWS Lightsail** using an Ubuntu server and GitHub.

## What is AWS Lightsail?

**AWS Lightsail** is a simplified cloud hosting service provided by Amazon Web Services (AWS). It allows developers to create virtual servers with a fixed monthly price and easily configure applications, networking, storage, and domains.

## Deployment Process

The basic deployment workflow was:

```text
GitHub Repository
       ↓
AWS Lightsail Instance
       ↓
Ubuntu Server
       ↓
Application Deployment
       ↓
Nginx / Reverse Proxy
       ↓
Domain
       ↓
HTTPS
```

## 1. Create a Lightsail Instance

First, an AWS Lightsail instance was created.

The instance was configured with:

* Platform: Linux/Unix
* Operating System: Ubuntu
* SSH access: Enabled
* Static IP: Configured

A **static IP** is important because the public IP should remain unchanged after restarting the server.

## 2. Connect to the Server

The server can be accessed using SSH:

```bash
ssh ubuntu@SERVER_IP
```

After connecting, the server was updated:

```bash
sudo apt update
sudo apt upgrade -y
```

## 3. Install Required Tools

Git was installed so the application could be cloned from GitHub:

```bash
sudo apt install git -y
```

Other dependencies such as Node.js, Java, Docker, or a database can be installed depending on the application stack.

## 4. Configure GitHub SSH Access

Instead of using GitHub credentials every time, an SSH key can be generated on the Lightsail server:

```bash
ssh-keygen -t ed25519 -C "lightsail-server"
```

The public key can be viewed using:

```bash
cat ~/.ssh/id_ed25519.pub
```

The public key was then added to the GitHub repository through:

```text
GitHub
→ Repository
→ Settings
→ Deploy keys
→ Add deploy key
```

A suitable title can be:

```text
YME AWS Server
```

The public SSH key is pasted into the **Key** field.

For deployment, the repository can then be cloned using SSH:

```bash
git clone git@github.com:USERNAME/REPOSITORY.git
```

## 5. Configure the Application

After cloning the repository:

```bash
cd REPOSITORY
```

The required environment variables were configured using an `.env` file or the appropriate application configuration.

Sensitive information such as:

* Database passwords
* API keys
* JWT secrets
* Cloud credentials

should never be committed to GitHub.

## 6. Configure the Firewall

Required ports were opened through the AWS Lightsail networking configuration.

Common ports include:

```text
22    SSH
80    HTTP
443   HTTPS
```

Application-specific ports should generally not be exposed publicly when the application can instead be accessed through Nginx.

For example:

```text
Internet
   ↓
Port 80/443
   ↓
Nginx
   ↓
Application Port
```

## 7. Configure Nginx

Nginx was used as a reverse proxy.

Example configuration:

```nginx
server {
    listen 80;
    server_name example.com;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

After modifying the configuration:

```bash
sudo nginx -t
```

If the configuration is valid:

```bash
sudo systemctl restart nginx
```

## 8. Connect the Domain

The domain DNS was configured to point to the Lightsail static IP.

For example:

```text
example.com → STATIC_IP
www.example.com → STATIC_IP
```

After DNS propagation, the domain could access the application through the server.

## 9. Enable HTTPS

HTTPS can be configured using Let's Encrypt and Certbot.

For Nginx:

```bash
sudo apt install certbot python3-certbot-nginx -y
```

Then:

```bash
sudo certbot --nginx -d example.com -d www.example.com
```

Certbot automatically configures the SSL certificate and can configure HTTP-to-HTTPS redirection.

## 10. Application Process Management

The application should continue running even after closing the SSH session.

For Node.js applications, PM2 can be used:

```bash
npm install -g pm2
```

Start the application:

```bash
pm2 start server.js
```

Save the process:

```bash
pm2 save
```

For Spring Boot applications, a systemd service or Docker can be used to keep the application running.

## 11. Updating the Application

When new changes are pushed to GitHub, the server can be updated:

```bash
cd /path/to/project
git pull origin main
```

Then rebuild/restart the application depending on the technology being used.

For example:

```bash
npm install
npm run build
pm2 restart all
```

or for a Spring Boot application:

```bash
./mvnw clean package
sudo systemctl restart application
```

## Important Lessons

### Static IP

A Lightsail static IP should be used instead of relying on a temporary public IP.

### SSH Deploy Keys

GitHub Deploy Keys allow the Lightsail server to securely access a private repository without storing a GitHub password.

### Nginx

Nginx can act as a reverse proxy and allows the application to remain on an internal port while exposing only ports 80 and 443 publicly.

### Environment Variables

Sensitive configuration should be stored outside the Git repository.

### HTTPS

Production applications should use HTTPS to encrypt communication between users and the server.

## Final Architecture

```text
                    ┌─────────────────┐
                    │     GitHub      │
                    │   Repository    │
                    └────────┬────────┘
                             │
                         SSH / Git
                             │
                             ↓
┌────────────────────────────────────────────────┐
│                 AWS Lightsail                  │
│                                                │
│  ┌──────────────┐                              │
│  │    Ubuntu    │                              │
│  │    Server    │                              │
│  └──────┬───────┘                              │
│         │                                      │
│         ↓                                      │
│  ┌──────────────┐                              │
│  │    Nginx     │ ← HTTP / HTTPS              │
│  └──────┬───────┘                              │
│         │                                      │
│         ↓                                      │
│  ┌──────────────┐                              │
│  │ Application  │                              │
│  │   Backend    │                              │
│  └──────┬───────┘                              │
│         │                                      │
│         ↓                                      │
│  ┌──────────────┐                              │
│  │   Database   │                              │
│  └──────────────┘                              │
│                                                │
└────────────────────────────────────────────────┘
                             ↑
                             │
                         Static IP
                             │
                             ↓
                         Domain Name
```

### Key Takeaway

Today I learned that hosting an application on AWS Lightsail involves more than simply running the application on a server. A proper production deployment requires **server configuration, SSH authentication, GitHub integration, firewall rules, Nginx reverse proxy configuration, DNS, HTTPS, and application process management**.
