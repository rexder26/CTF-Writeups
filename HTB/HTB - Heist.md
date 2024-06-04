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
![](https://i.imgur.com/9nIJJ4Z.png)

```shell
enable secret 5 $1$pdQG$o8nrSzsGXeaduXrjlvKc91 -> stealth1agent
!
username rout3r password 7 0242114B0E143F015F5D1E161713 -> $uperP@ssword
username admin privilege 15 password 7 02375012182C1A1D751618034F36415408 -> Q4)sJu\Y8qz*A3?d
```
![](https://i.imgur.com/qpXAsXJ.png)
![](https://i.imgur.com/mpRG1MZ.png)
- username - http://heist.htb/issues.php
### Gaining Access
![](https://i.imgur.com/yB6LwQU.png)
- Password Spraying is not working so i need to crack the another passwords.
	- so i tried to google the another hashes and i got cisco cracker(https://www.firewall.cx/cisco/cisco-routers/cisco-type7-password-crack.html)
		![](https://i.imgur.com/jN4ts95.png)
![](https://i.imgur.com/vlG7INY.png)
`Chase:Q4)sJu\Y8qz*A3?d`
## Internal
### Enumeration
![](https://i.imgur.com/FID1zQZ.png)
`evil-winrm -i 10.10.10.149 -u Chase -p 'Q4)sJu\\Y8qz*A3?d'
### Gaining Access
![](https://i.imgur.com/Gb8exnf.png)
- `Firefox credentials file exists at C:\Users\Chase\AppData\Roaming\Mozilla\Firefox\Profiles\77nc64t5.default\key4.db`
### Maintaining Access
![](https://i.imgur.com/dBAJJLv.png)
- i cant crack it with tools too
![](https://i.imgur.com/AkthAe3.png)
- So i try to check the processos
	- ![](https://i.imgur.com/JhoZJ0e.png)
![](https://i.imgur.com/8dyHy4i.png)
![](https://i.imgur.com/94oPBWu.png)
` Administrator : 4dD!5}x/re8]FBuZ `
# Random Notes