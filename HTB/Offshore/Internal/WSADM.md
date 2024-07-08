# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: 

# Findings
### Credentials
`FoundCREDs`

### Flags
- `OFFSHORE{4t_y0ur_5erv1ce}`
## External
### Enumeration
```
PORT     STATE SERVICE       REASON         VERSION
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack ttl 64
3389/tcp open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: CORP
|   NetBIOS_Domain_Name: CORP
|   NetBIOS_Computer_Name: WSADM
|   DNS_Domain_Name: corp.local
|   DNS_Computer_Name: WSADM.corp.local
|   DNS_Tree_Name: corp.local
|   Product_Version: 10.0.19041
|_  System_Time: 2024-07-02T13:05:13+00:00
```
- I tried to rdp to the user, but weird thing happened that the `wdadmin`
	- ![](https://i.imgur.com/4Lp7mY9.png)
	
![](https://i.imgur.com/lYpwAuq.png)
### Gaining Access
![](https://i.imgur.com/GxNt5Nz.png)
```shell
�����͹ PowerShell Settings
    PowerShell v2 Version: 2.0
    PowerShell v5 Version: 5.1.19041.1
    PowerShell Core Version:
    Transcription Settings:
    Module Logging Settings:
    Scriptblock Logging Settings:
    PS history file: C:\Users\ned.flanders_adm\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt
    PS history size: 1328B
    
�����͹ Vulnerable Leaked Handlers
� https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/leaked-handle-exploitation
�Getting Leaked Handlers, it might take some time...
  [X] Exception: System.Runtime.InteropServices.COMException (0x80070006): The handle is invalid. (Exception from HRESULT: 0x80070006 (E_HANDLE))
   at System.Runtime.InteropServices.Marshal.ThrowExceptionForHRInternal(Int32 errorCode, IntPtr errorInfo)
   at System.Runtime.InteropServices.Marshal.FreeHGlobal(IntPtr hglobal)
   at winPEAS.Native.Classes.UNICODE_STRING.Dispose(Boolean disposing)
    Handle: 2600(key)
    Handle Owner: Pid is 8848(winpeas) with owner: ned.flanders_adm
    Reason: AllAccess
    Registry: HKLM\software\microsoft\windowsruntime


�����͹ AV Information
    Some AV was detected, search for bypasses
    Name: Windows Defender
    ProductEXE: windowsdefender://
    pathToSignedReportingExe: %ProgramFiles%\Windows Defender\MsMpeng.exe
    whitelistpaths:     C:\Users\wsadmin\dControl\dControl\dControl\dControl

�����͹ Windows Defender configuration
  Local Settings

  Path Exclusions:
    C:\Users\wsadmin\dControl\dControl\dControl\dControl

  PolicyManagerPathExclusions:
    C:\Users\wsadmin\dControl\dControl\dControl\dControl
```
![](https://i.imgur.com/bhadm7k.png)
![](https://i.imgur.com/APmr9Cq.png)
![](https://i.imgur.com/3MiFMmB.png)
![](https://i.imgur.com/evYD2tW.png)
`Service 'WCAssistantService' (State: Running, StartMode: Auto) : C:\Program Files (x86)\Lavasoft\Web Companion\Application\Lavasoft.WCAssistant.WinService.exe`
- so i created a payload and replaced the binary then i get a reverse shell
![](https://i.imgur.com/7gBIugl.png)
![](https://i.imgur.com/o7z4GUB.png)
` justalocaladmin : Password123!`
```
* Username : wsadmin
	 * Domain   : CORP
	 * NTLM     : 669b12a3bac275251170afbe2c5de8c2
```
![](https://i.imgur.com/vmwOJuO.png)
![](https://i.imgur.com/3xIFubd.png)
` wsadmin: Workstationadmin1! `
![](https://i.imgur.com/mzKRLm5.png)
[[WS02]]
## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes