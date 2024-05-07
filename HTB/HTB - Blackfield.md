# Information
- CTF Name: 
- CTF Level:
- CTF Description: My 1st Owned Hard Machine but, i got this more like medium level
- Date: 
- Platform: 
- Category: #activedirectory #smb #ASREProasting #SeBackup #DCsync 

# Findings

## External
### Enumeration
![](https://i.imgur.com/OI2mFe3.png)
- `Crackmapexec` was not working
	- ![](https://i.imgur.com/mn7Z4Ln.png)
- I tried the smbclient and it did
	- ![](https://i.imgur.com/JqzLOJB.png)
- It is Invalid Login attack, i got access to `IPC` and `profiles`
	- ![](https://i.imgur.com/p4Bl2wd.png)
- i got usernames
	- ![](https://i.imgur.com/KGbOVp7.png)
- ![](https://i.imgur.com/REW9nJP.png)
```c
audit2020@blackfield.local
support@blackfield.local
svc_backup@blackfield.local
```

### Gaining Access
![](https://i.imgur.com/CG12FQY.png)
![](https://i.imgur.com/93ZeEDT.png)
`#00^BlackKnight  ($krb5asrep$support@BLACKFIELD.LOCAL)`
![](https://i.imgur.com/8CKxeGU.png)
![](https://i.imgur.com/6MqAtK4.png)
- ![](https://i.imgur.com/LjFVn0a.png)![](https://i.imgur.com/hKwWzpO.png)
![](https://i.imgur.com/mtl7YtY.png)


![](https://i.imgur.com/cK489qE.png)

## Internal
### Enumeration
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240427174428.png]]

### Gaining Access
- ![](https://i.imgur.com/ssDC4qI.png)
- ![](https://i.imgur.com/UdS0w0N.png)
![](https://i.imgur.com/oFTKHbX.png)
![](https://i.imgur.com/7wINucy.png)
### Maintaining Access
![](https://i.imgur.com/cPDogAs.png)
- Checked the permission and got backup operator
	- ![](https://i.imgur.com/32zxmAU.png)

- Created a script for diskshadow 
	- ![](https://i.imgur.com/8oGkpRU.png)

- Created a share and transfered the scrpt
	- ![](https://i.imgur.com/jirxDoj.png)
![](https://i.imgur.com/zRhkaxU.png)
![](https://i.imgur.com/xOA36wV.png)
![](https://i.imgur.com/r8sIscm.png)

![](https://i.imgur.com/8J1J4Dk.png)
![](https://i.imgur.com/OJPkqZ9.png)
# Random Notes