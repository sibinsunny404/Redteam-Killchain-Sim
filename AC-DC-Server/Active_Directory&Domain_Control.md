### 📝 **Active Directory & Domain Controller Setup Report**

**Project Title:** Active Directory Domain Configuration in Windows Server 2019
**Author:** Sibin Sunny
**Lab Environment:** Windows Server 2019 | Domain: `corp.local`
**Objective:** Configure an enterprise-grade AD Domain Controller, organize users via OUs, and apply domain-level Group Policies.

---

### 🔧 **Setup Overview**

As part of the full red team simulation project, I designed and deployed an **Active Directory Domain Controller** using **Windows Server 2019**, performing all essential configurations required for a realistic enterprise network environment.

---

### ✅ **Step-by-Step Implementation**

#### 1. **Server Promotion to Domain Controller**

* Installed the **Active Directory Domain Services (AD DS)** role via **Server Manager**.
* Promoted the server to a **Domain Controller** with the following configuration:

  * **Domain Name:** `corp.local`
  * **Forest & Domain Functional Level:** Windows Server 2016
  * **DNS Server:** Enabled
  * **Global Catalog:** Enabled
  * **Database, SYSVOL & Log paths:** Default

#### 2. **Active Directory Structure Setup**

* Used **Active Directory Users and Computers (ADUC)** to create the following:

  * **Organizational Units (OUs):**

    * `IT`
    * `HR`
    * `Sales`
  * **Users:**

    * Created individual domain users (`bob`, `alice`, etc.) and assigned them to the respective OUs.
  * **Groups:**

    * Domain Admins
    * Standard Users
    * Helpdesk

#### 3. **Group Policy Configuration**

* Configured **Group Policy Objects (GPOs)** to enforce:

  * **Password policies** (complexity, expiration)
  * **User restrictions** (no control panel, limited command access)
  * **Audit logging** and login banners
  * **Firewall and Defender settings**

#### 4. **DNS & Network Configuration**

* Verified and updated **DNS zones** to support name resolution within the domain.
* Ensured proper hostname resolution and reverse lookup configuration.

#### 5. **Domain Join & Validation**

* Joined multiple Windows clients (e.g., Windows 10 machines) to the `corp.local` domain.
* Verified login permissions, GPO application, and domain user access across the network.

---

### 🔒 Security Considerations

* Ensured domain controller services were hardened and monitored.
* User permissions were set with the principle of least privilege.
* Enabled Windows Defender & logging for account and system events.

---

### 📌 Outcome

> Successfully created a fully functional **Active Directory Domain Controller** with structured users, roles, and Group Policies. This setup served as the foundation for red team attack simulation and SIEM-based detection in subsequent phases of the cybersecurity project.
