
🔓 Phase 2 – Initial Access Report (with MITRE ATT&CK Mapping and Custom Wordlist Cracking)
Author: Sibin Sunny  
Date: July 4, 2025  


🧪 Lab Description:
This stage of the red team simulation was executed in a virtual lab with:
- Kali Linux attacker machine (192.168.50.10)
- Windows Server 2019 domain controller (192.168.50.5)
- Windows 10 client machine (192.168.50.20)
- All VMs on bridged network (192.168.50.0/24)
- Goal: Capture valid credentials or usable hashes to simulate gaining initial access


🔹 Tool Used: Responder
Command: sudo responder -I eth0
✅ LLMNR and NBT-NS spoofing was enabled

🔹 Triggering Victim:
Manual action from victim system to access: \abc or \randomshare  
✅ NTLMv2 hash was successfully captured by Responder

Captured NTLMv2 Hash:
```
Victim::DESKTOP-1M82OOV:b1a6ac6a6cad149d:56B5F06F0EAF37C02FBCD06A9ED2BE12:...
```

🔹 Hash Cracking Attempts

| Tool      | Wordlist Used                                  | Result           |
|-----------|-------------------------------------------------|------------------|
| hashcat   | rockyou.txt                                     | ❌ No match      |
| john      | rockyou.txt                                     | ❌ No match      |
| hashcat   | SecLists/common-passwords-win.txt               | ❌ No match      |
| hashcat   | ❗ Custom wordlist created for this hash         | ✅ Password Cracked |

⚠️ Note: The hash was cracked using a **custom wordlist created by the attacker** (knowing the password beforehand).  
This is useful for documentation, but **in a real-world scenario this would be unknown**, so **Phase 3 will proceed using pass-the-hash only**, not the cracked password.

✅ Phase Objective Achieved: Captured and validated NTLMv2 hash usable for authentication


MITRE ATT&CK Techniques Used:
- T1557.001: LLMNR/NBT-NS Poisoning – Using Responder to capture hashes through broadcast spoofing
- T1110.003: Password Cracking – Cracked captured NetNTLMv2 hash using a custom wordlist
- T1078: Valid Accounts – Credential foothold achieved using valid hash (will be used in pass-the-hash attack)


📌 Phase 2 Summary

| Step | Description                      | Result      |
|------|----------------------------------|-------------|
| 2.1  | Responder Setup                  | ✅ Success   |
| 2.2  | Triggered LLMNR/NBTNS Broadcast | ✅ Success   |
| 2.3  | NTLMv2 Hash Capture              | ✅ Captured  |
| 2.4  | Hash Cracking Attempted         | ✅ Done      |
| 2.5  | Cracked Password (for doc)      | ✅ Found     |
| 2.6  | Credential Foothold Gained      | ✅ Yes       |

🧠 Attacker’s Insight:
Even without cracking the hash in a real-world case, the NTLMv2 hash captured is valid and will be leveraged using pass-the-hash techniques in the next phase.

✅ Next Phase: Phase 3 – Execution (Authenticate using the captured NTLMv2 hash)

