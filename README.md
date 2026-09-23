# Windows Server 2022 – Active Directory & Domain Services Lab

## 📌 Project Overview

This project documents a hands-on **Windows Server 2022 Active Directory lab environment** built to practise core systems administration and IT Support skills.

The lab covers the configuration of a **Domain Controller**, **Active Directory Domain Services (AD DS)**, integrated **DNS**, a domain-joined **File Server**, static IP addressing, hostname configuration, domain promotion, and domain membership.

The objective was to build a small Windows domain environment that demonstrates practical troubleshooting and administration tasks commonly encountered in **L1/L2 IT Support and Service Desk** roles.

---

## 🖥️ Lab Environment

| Component            | Configuration                   |
| -------------------- | ------------------------------- |
| Operating System     | Windows Server 2022             |
| Domain Controller    | Admin                           |
| Domain Controller IP | `192.168.96.134/24`             |
| File Server          | FS                              |
| File Server IP       | `192.168.96.135/24`             |
| Domain               | `sagartech.local`               |
| NetBIOS Domain       | `SAGARTECH`                     |
| DNS                  | Active Directory-integrated DNS |
| Virtual Environment  | Virtual Machine Lab             |

---

## 🏗️ Lab Architecture

```text
                    Windows Server 2022
                           │
                           │
                  ┌────────▼────────┐
                  │  Domain         │
                  │  Controller     │
                  │  Admin          │
                  │ 192.168.96.134  │
                  │                 │
                  │ AD DS + DNS     │
                  └────────┬────────┘
                           │
                    SAGARTECH.local
                           │
                  ┌────────▼────────┐
                  │   File Server   │
                  │       FS        │
                  │ 192.168.96.135  │
                  │                 │
                  │ Domain Joined  │
                  └─────────────────┘
```

---

# 🔧 Configuration & Implementation

## 1. Network Configuration

Before installing server roles, the network configuration was standardised to ensure reliable communication between machines.

### Domain Controller

Configured the Domain Controller with:

* Static IP address: `192.168.96.134/24`
* Gateway: `192.168.96.2`
* DNS pointing to the server itself
* DHCP disabled
* Hostname: `Admin`

The configuration was verified using:

```powershell
ipconfig /all
```

A static address was used so that clients could reliably locate the Domain Controller through DNS.

---

## 2. File Server Configuration

Configured the File Server on the same subnet as the Domain Controller.

### Configuration

* Static IP: `192.168.96.135/24`
* DNS pointing to the Domain Controller
* Hostname: `FS`
* Same network/subnet as the Domain Controller

Connectivity and network configuration were verified before attempting the domain join.

---

# 🏢 Active Directory Domain Services

## 3. Installing AD DS

The **Active Directory Domain Services** role was installed through:

```text
Server Manager
→ Add Roles and Features
→ Active Directory Domain Services
```

The required management tools were also installed, including:

* Group Policy Management
* Active Directory Administrative Center
* AD DS management tools
* Active Directory PowerShell module

---

## 4. Promoting the Server to a Domain Controller

After installing AD DS, the server was promoted to a Domain Controller.

A new forest was created for the lab environment.

### Domain Configuration

```text
Domain:       sagartech.local
NetBIOS:      SAGARTECH
Server:       Admin
```

The configuration included:

* New Active Directory forest
* DNS installation
* Global Catalog
* Windows Server 2016 functional level
* Directory Services Restore Mode (DSRM) password
* Prerequisite validation

After successful promotion, the server restarted to initialise:

* Active Directory database
* SYSVOL
* Global Catalog services

The Domain Administrator account was then used to verify successful domain operation.

---

# 🔗 File Server Domain Join

## 5. Joining FS to the Domain

The File Server was moved from a workgroup into the Active Directory domain.

```text
FS
  ↓
System Properties
  ↓
Computer Name
  ↓
Domain
  ↓
sagartech.local
```

The domain join was authorised using Domain Administrator credentials.

After restarting the File Server, domain membership was verified.

Expected FQDN:

```text
FS.sagartech.local
```

---

# 🧪 Skills Practised

This lab provided hands-on practice with:

### Systems Administration

* Windows Server 2022
* Server configuration
* Server hostname management
* Static IP configuration
* Server reboot and post-configuration verification

### Active Directory

* Active Directory Domain Services
* Domain Controller deployment
* New forest creation
* Domain configuration
* NetBIOS naming
* Global Catalog
* SYSVOL
* Domain Administrator authentication

### Networking

* IPv4 configuration
* Static addressing
* Subnet configuration
* Default gateway
* DNS configuration
* Server-to-server connectivity
* Domain DNS requirements

### Domain Management

* Domain joining
* Computer account/domain membership
* Domain authentication
* FQDN verification
* Workgroup-to-domain transition

### Troubleshooting & Verification

* `ipconfig /all`
* Network configuration validation
* DNS configuration verification
* Hostname verification
* Domain membership verification
* AD DS prerequisite checks

---

# 📸 Screenshots

Screenshots documenting the implementation are included in the project documentation.

Recommended screenshot structure:

```text
screenshots/
│
├── 01-static-ip-dc.png
├── 02-dc-ipconfig.png
├── 03-dc-hostname.png
├── 04-file-server-network.png
├── 05-file-server-hostname.png
├── 06-ad-ds-installation.png
├── 07-ad-ds-tools.png
├── 08-domain-controller-promotion.png
├── 09-domain-configuration.png
├── 10-ad-prerequisite-check.png
├── 11-domain-admin-login.png
└── 12-file-server-domain-join.png
```

---

# 📄 Project Documentation

Detailed step-by-step documentation is available in:

**`labb.docx`**

The document contains the configuration process, verification steps and screenshots for the lab implementation.

---

# 🎯 IT Support Relevance

This project was created to develop practical skills relevant to **L1/L2 IT Support, Service Desk and Junior Systems Administration** roles.

The lab demonstrates experience with:

* Windows Server environments
* Active Directory
* Domain authentication
* DNS fundamentals
* TCP/IP configuration
* User and computer domain environments
* Server troubleshooting
* Domain joining
* Technical documentation
* Configuration verification
* Structured troubleshooting

These are foundational technologies frequently encountered when supporting Windows-based business environments.

---

# 🔍 Troubleshooting Approach

The lab followed a structured troubleshooting process:

```text
1. Identify the problem
        ↓
2. Check network configuration
        ↓
3. Verify IP address and gateway
        ↓
4. Verify DNS configuration
        ↓
5. Verify hostname
        ↓
6. Check domain configuration
        ↓
7. Perform the required change
        ↓
8. Restart where required
        ↓
9. Verify the result
        ↓
10. Document the configuration
```

This approach helps ensure that configuration changes are validated rather than assumed to be successful.

---

# 🚀 Future Lab Expansion

Future phases of this lab can extend the environment with:

* Active Directory users and groups
* Organizational Units (OUs)
* Group Policy Objects (GPOs)
* Password policies
* Account lockout and password-reset scenarios
* File shares and NTFS permissions
* DHCP Server
* DNS troubleshooting
* Windows 11 domain client
* Microsoft 365 administration
* Microsoft Entra ID
* Intune
* PowerShell automation
* VPN troubleshooting
* Endpoint management
* Common Service Desk troubleshooting scenarios

---

## 📚 Documentation

**Detailed lab guide:** `labb.docx`

**Environment:** Windows Server 2022 virtual lab

**Primary technologies:** Active Directory Domain Services, DNS, Windows Server 2022, IPv4, Domain Services

---

## 👨‍💻 Portfolio Purpose

This project is part of my hands-on IT Support and Systems Administration portfolio, demonstrating practical experience with Windows-based infrastructure, domain environments, networking fundamentals, troubleshooting and technical documentation.
