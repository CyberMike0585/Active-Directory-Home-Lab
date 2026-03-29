# Active Directory Home Lab (Windows Server + Windows 11)

## 📌 Project Overview

This project demonstrates the deployment of a small-scale enterprise Active Directory environment using Windows Server and a Windows 11 client. The lab simulates real-world IT infrastructure, including centralized authentication, file sharing, and access control.

---

## 🧱 Environment Setup

### 🔧 Infrastructure

* Hypervisor: Proxmox VE
* Domain Controller: Windows Server
* Client Machine: Windows 11 Pro

### 🌐 Network Configuration

* Static IP assigned to Domain Controller
* DNS configured to point to Domain Controller
* Client machine configured to use Domain Controller for DNS resolution

---

## ⚙️ Key Configurations

### 🏢 Active Directory Setup

* Installed Active Directory Domain Services (AD DS)
* Promoted server to Domain Controller
* Created domain:

```plaintext
MGEnterprise.local
```

---

### 📂 Organizational Structure

Created Organizational Units (OUs):

* Corp-Users
* Corp-Computers
* Groups
* Servers

---

### 👥 User & Group Management

Created domain users and security groups:

#### Users:

* Nestor Gibbs
* John Smith
* Test User

#### Groups:

* IT_Admins
* HR
* Sales
* SharedDrive_RO
* SharedDrive_RW

Users were assigned to appropriate groups to simulate role-based access control (RBAC).

---

### 💾 File Server Configuration

* Created shared folder:

```plaintext
C:\Shared
```

* Configured SMB share:

```plaintext
\\WIN-DC-01\Shared
```

* Created subfolders:
* HR
* Sales
* Public

---

### 🔐 Permissions Configuration

#### Share Permissions:

* Configured access using security groups

#### NTFS Permissions:

* Applied group-based permissions to restrict access:

  * HR group → HR folder
  * Sales group → Sales folder
  * Domain Users → Public folder

---

### 🖥️ Client Configuration

#### Windows 11 Setup:

* Installed Windows 11 Pro
* Installed VirtIO drivers (disk + network)

#### Domain Join:

* Joined client to:

```plaintext
MGEnterprise.local
```

#### Authentication Test:

Verified login using domain credentials:

```cmd
whoami
```

---

### 🔗 Network Drive Mapping

Mapped shared drive for users:

```plaintext
Z: → \\WIN-DC-01\Shared
```

---

## 🧪 Troubleshooting & Issues Resolved

### ❌ Issue: Disk not detected during Windows install

* Cause: Missing VirtIO storage driver
* Fix:

  * Loaded correct driver:

  ```plaintext
  vioscsi\w11\amd64
  ```

---

### ❌ Issue: Network adapter not working

* Cause: Missing VirtIO network driver
* Fix:

  ```plaintext
  NetKVM\w11\amd64
  ```

---

### ❌ Issue: Could not join domain

* Cause: Incorrect DNS configuration
* Fix:
* Set client DNS to Domain Controller IP

---

### ❌ Issue: Access denied to shared folder

* Cause: NTFS and Share permissions mismatch
* Fix:
* Configured both:

  * Share permissions
  * NTFS permissions

---

### ❌ Issue: Cannot delete OU (accidental protection)

* Cause: “Protect from accidental deletion” enabled
* Fix:
* Disabled protection via Object tab

---

### ❌ Issue: Domain join blocked after rename

* Cause: Restart required after renaming PC
* Fix:
* Restarted system before joining domain

---

## 📸 Screenshots

Screenshots included in `/screenshots` folder:

* Active Directory OU structure
* Users and groups
* Domain-joined client
* Command prompt (`whoami`)
* Shared folder access
* Network drive mapping
* Permissions configuration

---

## 🧠 Skills Demonstrated

* Active Directory Domain Services (AD DS)
* DNS configuration and troubleshooting
* User and group management
* Role-based access control (RBAC)
* SMB file sharing
* NTFS & share permissions
* Windows client domain join
* Virtualization (Proxmox)
* Troubleshooting real-world IT issues

---

## 🚀 Key Takeaways

This project simulates real-world helpdesk and system administration tasks, including:

* Managing domain environments
* Troubleshooting authentication issues
* Configuring secure file access
* Supporting end-user environments

---

## 📎 Future Improvements

* Group Policy (GPO) automation
* Logon scripts
* Password policies
* Multi-client environment
* Backup and recovery integration
