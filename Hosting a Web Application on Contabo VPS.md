# TIL: Hosting a Web Application on Contabo VPS

📅 Date: 2026-08-26

Today I learned how to **deploy and host a web application on a Contabo VPS**.

A **VPS (Virtual Private Server)** provides a remote server environment where applications can be deployed, configured, and accessed over the internet.

## What I Learned

* **VPS Deployment** – Learned how to deploy a web application to a Contabo VPS.
* **SSH Access** – Learned how to securely connect to and manage the remote server.
* **Server Configuration** – Learned how to configure the server environment required to run the application.
* **Application Hosting** – Learned how to run a web application on a production server.
* **Networking** – Learned how to configure server ports and allow external access.
* **Server Management** – Gained practical experience managing a Linux-based VPS.
* **Deployment Workflow** – Understood the process of moving an application from development to production.

## VPS Hosting Workflow

```text
Local Development
       │
       ▼
    GitHub
       │
       ▼
  Contabo VPS
       │
       ├──► Server Configuration
       ├──► Application Setup
       ├──► Dependencies
       └──► Application Running
               │
               ▼
            Internet
               │
               ▼
             Users
```

## Key Takeaway

> **A VPS provides a flexible environment for deploying and continuously hosting web applications on a remote server accessible over the internet.**

In simple terms:

```text
Application → Contabo VPS → Server Configuration → Internet → Users
```
