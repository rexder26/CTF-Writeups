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
![](https://i.imgur.com/7pFLL02.png)
- Users
	- Ruy Alonso
	- Maya Bendito
	- Gregory Smith
- We got LFI
	- ![](https://i.imgur.com/B99qFhR.png)

	- ![](https://i.imgur.com/jTasPIH.png)
- `..\..\..\..\..\..\..\..\WINDOWS/system32/drivers/etc/hosts`
- ![](https://i.imgur.com/rJAAN5H.png)
![](https://i.imgur.com/ZIkYYNX.png)
`ruy@mailing.htb`
https://www.exploit-db.com/exploits/7012
![](https://i.imgur.com/qVmyNED.png)

![](https://i.imgur.com/susHJij.png)
```shell
[Directories]
ProgramFolder=C:\Program Files (x86)\hMailServer
DatabaseFolder=C:\Program Files (x86)\hMailServer\Database
DataFolder=C:\Program Files (x86)\hMailServer\Data
LogFolder=C:\Program Files (x86)\hMailServer\Logs
TempFolder=C:\Program Files (x86)\hMailServer\Temp
EventFolder=C:\Program Files (x86)\hMailServer\Events
[GUILanguages]
ValidLanguages=english,swedish
[Security]
AdministratorPassword=841bb5acfa6779ae432fd7a4e6600ba7
[Database]
Type=MSSQLCE
Username=
Password=0a9f8ad8bf896b501dde74f08efd7e4c
PasswordEncryption=1
Port=0
Server=
Database=hMailServer
Internal=1
```
![](https://i.imgur.com/2kwA2Jk.png)
` Administratrot pass : homenetworkingadministrator `
- Based on the `instruction.pdf` file, i installed thunderbird and used the password i got with `administrator@mailing.htb` email
	- ![](https://i.imgur.com/5cnv59x.png)

	- ![](https://i.imgur.com/4D8MIW7.png)

- We got another user
	- ![](https://i.imgur.com/QBqlB5r.png)
- But there is nothing on th account, sp i tried to go back to the another hash we got.
	- ![](https://i.imgur.com/nttXHa9.png)
- https://github.com/GitMirar/hMailDatabasePasswordDecrypter ![](https://i.imgur.com/kSSXbiJ.png)
-  we got another password`"6FC6F69152AD"` but tried to login with maya,user,ruy but it doesnt work.
- So i  searched for latest CVE on Outlook and thunderbird, and i got the outlook
	- ![](https://i.imgur.com/GWvwqXG.png)
-  ![](https://i.imgur.com/WiaO3f7.png)
- ![](https://i.imgur.com/dGK906R.png)
- ![](https://i.imgur.com/YmLI5FL.png)
- ` maya : m4y4ngs4ri `
### Gaining Access
![](https://i.imgur.com/Wf7UBMK.png)
## Internal
### Enumeration
![](https://i.imgur.com/jTcOfB5.png)
![](https://i.imgur.com/3g60bsX.png)
![](https://i.imgur.com/H2xynrf.png)
![](https://i.imgur.com/NPzYbcj.png)
- We have the From the files insalled and the script we have my attention was grabed by libreoffie `C:\Users\localadmin\Documents\scripts\soffice.ps1` 
	- ![](https://i.imgur.com/x6Pp5Qe.png)

- ![](https://i.imgur.com/eBoYz4y.png)
- ![](https://i.imgur.com/65FgWXE.png)
	- Tried to Narrow it down. ![](https://i.imgur.com/swjgeN5.png)

- ![](https://i.imgur.com/3CwB0sG.png)
- So what i understand is there is the script from `localadmin` user was tring to run the script from the public/document i though the script was dublicate
![](https://i.imgur.com/4Weymft.png)
- so i thought to put the odt file here.
### Gaining Access

![](https://i.imgur.com/AulvAeo.png)
![](https://i.imgur.com/yrg6NdM.png)
- After some min, i got admin group as u see.
![](https://i.imgur.com/kuKNNzz.png)
- Tried to do winrm with admin but that didnt worked
	- ![](https://i.imgur.com/ZifPRxr.png)
	- ![](https://i.imgur.com/ubcbfrh.png)

- Tried with `localadmin`
	- ![](https://i.imgur.com/4fS8iun.png)


### Maintaining Access

![](https://i.imgur.com/BXuiNtW.png)

# Random Notes