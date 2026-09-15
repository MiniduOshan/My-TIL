# TIL — Microsoft Active Directory

📅 **Date:** 2026-09-15

## What I Learned

Today I learned about **Microsoft Active Directory (AD)** and how it is used to manage users, computers, domains, and network resources in a Windows environment.

Active Directory provides a centralized way to manage and authenticate users and devices within an organization.

## Key Concepts

### 1. Domain

A **domain** is a logical environment where users, computers, and other resources are centrally managed.

Example:

```text
minidu.com
```

### 2. Domain Controller

A **Domain Controller (DC)** is a Windows Server that runs Active Directory Domain Services (AD DS).

It is responsible for:

* User authentication
* User and computer management
* Applying security policies
* Managing domain resources

### 3. Active Directory Domain Services (AD DS)

**AD DS** stores information about objects in the domain, such as:

* Users
* Computers
* Groups
* Organisational Units (OUs)

### 4. Organisational Unit (OU)

An **OU** is used to organise users and computers inside a domain.

Example:

```text
minidu.com
│
├── Students
├── Staff
├── Computers
└── Servers
```

OUs can also be used to apply **Group Policies** to specific users or computers.

### 5. DNS and Active Directory

DNS is very important in Active Directory.

Active Directory uses DNS to locate domain controllers and other domain services.

For example:

```text
minidu.com
```

A DNS server can contain records such as:

* **A record** — Maps a hostname to an IP address
* **CNAME** — Creates an alias for another hostname
* **PTR record** — Used for reverse DNS lookup

Example:

```text
server.minidu.com → 192.168.1.10
```

Reverse lookup:

```text
192.168.1.10 → server.minidu.com
```

### 6. Users and Groups

Active Directory allows administrators to create users and groups.

Example:

```text
Users
 ├── Minidu
 ├── Admin
 └── Student

Groups
 ├── IT-Admins
 ├── Students
 └── Developers
```

Groups make it easier to assign permissions to multiple users.

### 7. Group Policy

**Group Policy** allows administrators to centrally configure settings for users and computers.

Examples:

* Password policies
* Security settings
* Software restrictions
* Windows configuration
* Desktop settings

## Basic Active Directory Structure

```text
                    Domain Controller
                          │
                          ▼
                     minidu.com
                          │
        ┌─────────────────┼─────────────────┐
        │                 │                 │
       Users           Computers          Groups
        │                 │                 │
     Minidu           Windows PC        IT-Admins
     Admin            Server            Students
```

## Important Commands

### Check IP configuration

```cmd
ipconfig
```

### Test DNS

```cmd
nslookup minidu.com
```

### Test network connectivity

```cmd
ping minidu.com
```

### Check domain information

```cmd
systeminfo
```

### Check current user

```cmd
whoami
```

## Key Takeaways

* **Active Directory** provides centralised management of Windows environments.
* **Domain Controllers** manage authentication and domain services.
* **DNS is essential** for Active Directory.
* **OUs** help organise users and computers.
* **Groups** simplify permission management.
* **Group Policy** allows centralised configuration and security management.

## What I Practised

Today I practised working with a Windows Server Active Directory environment by:

* Creating an Active Directory domain
* Configuring DNS
* Creating host records
* Working with CNAME records
* Understanding reverse DNS / PTR records
* Connecting a Windows client to the domain
* Troubleshooting domain and DNS resolution issues

---

### TIL Summary

> **Active Directory + DNS + Domain Controller** work together to provide centralised identity, authentication, and resource management in a Windows network.
