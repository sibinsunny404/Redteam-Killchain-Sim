
🔒 Phase 1 – Internal Reconnaissance Report (with MITRE ATT&CK Mapping)
Author: Sibin Sunny  
Date: July 2, 2025  


🧪 Lab Description:
This red team simulation was executed in a virtualized test lab consisting of:
- One Kali Linux attacker machine (192.168.50.10)
- One Windows Server 2019 domain controller (192.168.50.5)
- One Windows 10 client (192.168.50.20)
- All VMs connected via Host-only network in the 192.168.50.0/24 subnet
- Purpose: Simulate the internal recon phase of an Active Directory environment as part of a full kill chain project


🔹 Network Overview
| Hostname         | IP Address      | MAC Address        | Role                 |
|------------------|-----------------|---------------------|----------------------|
| Gateway/Router   | 192.168.50.1    | 00:50:56:C0:00:01   | Network gateway      |
| Kali Linux       | 192.168.50.10   | -                   | Attacker machine     |
| Windows DC       | 192.168.50.5    | 00:0C:29:96:9E:AE   | Domain Controller    |
| Windows 10 Client| 192.168.50.20   | 00:0C:29:DD:1B:DA   | Client machine       |

🔹 Host Discovery (Nmap)
Command: sudo nmap -sn 192.168.50.0/24  
✅ Result: 4 hosts detected on the subnet.

🔹 Port Scanning & Service Enumeration
Command: nmap -sV -p- -Pn 192.168.50.5 --system-dns  
✅ DC has common AD ports open (389, 445, 88, 5985, etc.)

🔹 Domain Discovery (enum4linux-ng)
Command: sudo enum4linux-ng 192.168.50.5  
✅ Identified Domain: corp.local  
✅ Hostname: WIN-JI79TC0RNC0  
✅ OS: Windows Server 2019 (Build 17763)  
✅ Null SMB login allowed  
❌ User/Group/Share enumeration blocked

🔹 LDAP Enumeration Attempt
Command: ldapsearch -x -H ldap://192.168.50.5 -b "dc=corp,dc=local"  
❌ Anonymous LDAP bind failed – Expected for hardened AD setups

🔹 CrackMapExec Check
Command: crackmapexec smb 192.168.50.5 --users  
❌ No usernames returned

📌 Phase Summary
| Task                  | Result     |
|-----------------------|------------|
| Host Discovery        | ✅ Success |
| Port Scan             | ✅ Success |
| Domain Discovery      | ✅ Success |
| User Enumeration      | ❌ Blocked |
| Share Enumeration     | ❌ Blocked |
| Null Session Access   | ✅ Success |
| LDAP Bind             | ❌ Blocked |
| RPC Access            | ❌ Blocked |


MITRE ATT&CK Techniques Used:
- T1087: Account Discovery – Attempted user enumeration via SMB/LDAP
- T1135: Network Share Discovery – Checked accessible shares via smbclient and enum4linux-ng
- T1046: Network Service Scanning – Used nmap to identify open ports/services
- T1069: Permission Groups Discovery – Attempted to enumerate domain groups and users


📸 Screenshots
Screenshots are recommended to visually validate execution (e.g., terminal outputs, tools).

✅ Next Phase: Proceed to Initial Access – Hash capture (Responder), password guessing, or exploit delivery.
