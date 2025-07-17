#### Blue Team Detection Report using Wazuh SIEM



Objective: Detect and log the adversarial actions performed during the Red Team Kill Chain Simulation using Wazuh SIEM.



Environment:



Wazuh Manager and Dashboard running on Ubuntu

Agent installed on Windows Domain Controller and victim machines

MITRE ATT\\\&CK module enabled



🔍 Detection Summary (MITRE ATT\\\&CK Correlation)



The following tactics and techniques were successfully detected:



| Tactic                   | Techniques Detected          | Description                                       |

| ------------------------ | ---------------------------- | ------------------------------------------------- |

| \*\*Initial Access\*\*       | T1078 - Valid Accounts       | Successful login using stolen credentials         |

| \*\*Persistence\*\*          | T1547.001 - Registry Run Key | Registry key used for startup reverse shell       |

| \*\*Privilege Escalation\*\* | T1078, T1547.001             | Local admin privilege abuse and persistence setup |

| \*\*Credential Access\*\*    | T1003.001 - LSASS Memory     | Procdump used to dump LSASS and extract secrets   |

| \*\*Lateral Movement\*\*     | T1550.002 - Pass the Hash    | Hash used to authenticate to other hosts          |

| \*\*Defense Evasion\*\*      | T1070.004 - File Deletion    | Cleanup of logs, files, and traces                |





📊 Wazuh Dashboard Overview



Top Tactics Visualized:



&nbsp;  Defense Evasion

&nbsp; \* Privilege Escalation

&nbsp; \* Initial Access

&nbsp; \* Persistence

&nbsp; \* Lateral Movement



\* \*\*Rule Level by Attack:\*\*



&nbsp; \* Multiple alerts associated with MITRE rules, rule level 3 and 6

&nbsp; \* Most alerts triggered under Valid and Domain Accounts activity



\* \*\*MITRE ATT\\\&CK Events:\*\*



&nbsp; \* All key activities shown as alerts with tactic categories

&nbsp; \* Rule `60106` was triggered multiple times indicating credential-based logins (T1078)



\* \*\*Agent and Event Data:\*\*



&nbsp; \* Monitored via Windows agent ID `001`

&nbsp; \* Successful logon sessions from CORP\\Administrator were flagged

&nbsp; \* `data.win.eventdata` fields showed impersonation level, logon process, source IPs



---



\### 📁 Screenshots \& Artifacts Collected



\* Wazuh MITRE ATT\\\&CK dashboard snapshot

\* Event logs showing detection of each phase

\* Rule IDs, severity, and technique IDs stored

\* Dashboards showing tactics distribution and alert counts



---



\### ✅ Detection Verification



Each red team attack phase was followed by confirmation of alerts in Wazuh:



\* Execution of reverse shell via `wmiexec.py` ➝ Triggered T1078

\* LSASS dump via `procdump.exe` ➝ Triggered T1003.001

\* User creation and registry key persistence ➝ Triggered T1547.001

\* Pass-the-hash SMB login via `crackmapexec` ➝ Triggered T1550.002



---



\### 🔐 Conclusion



Wazuh successfully detected multiple stages of the red team attack chain. The MITRE ATT\\\&CK plugin provided effective categorization of tactics and techniques, while correlated events offered full visibility into attacker actions.



This validates Wazuh as an effective lightweight SIEM for both detection and response in a lab-based security simulation.



Let me know if you'd like this exported as a PDF or combined with the full kill chain simulation report.



