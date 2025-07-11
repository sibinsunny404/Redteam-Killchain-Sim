# Full Red Team Kill Chain Simulation in Active Directory with Wazuh Detection (MITRE Mapped)

## Author: Sibin Sunny

**Certification**: Certified Ethical Hacker (CEH)  
**Type**: Red Team Simulation + Blue Team Detection  
**Platform**: Kali, Ubuntu, Windows Server 2019, Windows 10  
**SIEM Tool**: Wazuh  
**Framework**: MITRE ATT&CK

---

## 🛠️ Lab Environment Setup

- Configured Windows Server 2019 as Domain Controller (DC)
- Created Active Directory users, OUs, applied Group Policies, and assigned roles
- Installed Wazuh manager on Ubuntu and configured Wazuh agent on all Windows machines

---

## 🔎 Phase 1: Reconnaissance (TA0043)
- Used tools like `nmap`, `crackmapexec`, and `enum4linux`
- Identified open ports, OS version, shares, and domain info

---

## 🎯 Phase 2: Initial Access (TA0001)
- Captured NTLMv2 hashes using `Responder`
- Cracked hashes with `hashcat`
- Verified credentials via `crackmapexec`

---

## 💻 Phase 3: Execution (TA0002)
- Executed remote commands using Impacket's `wmiexec.py`
- Gained shell access with PowerShell reverse shell

---

## ⬆️ Phase 4: Privilege Escalation (TA0004)
- Verified privileges via `whoami /priv`
- Saved and exfiltrated SAM, SYSTEM, SECURITY hives
- Used `secretsdump.py` to dump hashes and extracted Domain Admin

---

## 🧪 Phase 5: Credential Access & Lateral Movement (TA0006, TA0008)
- Moved laterally using `psexec.py`, `smbexec.py`, and `wmiexec.py`
- Verified `NT AUTHORITY\SYSTEM` access

---

## 📡 Phase 6: Command & Control (TA0011)
- Set up listener using `nc -lvnp 4444`
- Launched reverse shell using PowerShell payload

---

## 🎯 Phase 7: Actions on Objectives (TA0009)
- Exfiltrated `Top_Secrets.txt` via Python HTTP server
- Established persistence using:
  - Registry Run key
  - Admin account creation
  - Scheduled Task
- Dumped LSASS for further credential access

---

## 📊 Phase 8: Detection & Logging with Wazuh

- Configured Wazuh SIEM for monitoring
- Detected techniques:
  - **T1078** - Valid Accounts
  - **T1550.002** - Pass the Hash
  - **T1003.001** - LSASS Dumping
  - **T1547.001** - Registry Persistence
- MITRE Dashboard revealed tactic-wise categorization
- Screenshots and logs were saved

---

## 📁 Evidence & Artifacts
- Screenshots of every attack step
- Hashes and shell output logs
- `.txt` reports per phase
- Wazuh alert logs and dashboards

---

## 🧰 Tools Used

**Red Team**: crackmapexec, Responder, Impacket, PowerShell, mimikatz  
**Blue Team**: Wazuh  
**Platform**: Windows Domain (AD), Ubuntu, Kali

---

## 🚀 Outcome
Successfully simulated a full red team attack chain on a Windows AD network and monitored each attack using Wazuh mapped to MITRE ATT&CK tactics. This lab setup showcases both offensive and defensive skills for cybersecurity portfolios.

---

> 💡 This project is a complete offensive + detection simulation suitable for showcasing on GitHub, LinkedIn, or personal cybersecurity portfolios.

