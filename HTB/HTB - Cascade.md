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
![](https://i.imgur.com/HnySOSs.png)
![](https://i.imgur.com/bt2A58c.png)
![](https://i.imgur.com/Fmd5fmy.png)
![](https://i.imgur.com/Qk3pmRN.png)
![](https://i.imgur.com/b1GOHtN.png)
![](https://i.imgur.com/YDwgLIv.png)
- The password properties value of 0x00000000 suggests that there are no additional password complexity requirements or restrictions in place. This means that the password policy does not enforce any specific requirements such as the use of uppercase letters, lowercase letters, numbers, or special characters.
![](https://i.imgur.com/23Pnce8.png)
![](https://i.imgur.com/n96TYuf.png)
![](https://i.imgur.com/ddk5k2T.png)
- ` r.thompson : rY4n5eva `
![](https://i.imgur.com/v5MiUdv.png)
![](https://i.imgur.com/53NqyLl.png)
![](https://i.imgur.com/lhmZv8y.png)
![](https://i.imgur.com/k3tUXCe.png)
![](https://i.imgur.com/GiD7hrd.png)
![](https://i.imgur.com/MHJg9Jq.png)
https://github.com/frizb/PasswordDecrypts
- As you see the text file we got is a registry file for the `tightvnc` so at 1st i tried to decode the password to bc i thought it is hex, but that failed me, so i tried to look for tighvnc decode.
	- ![](https://i.imgur.com/fURD0wS.png)
	- ![](https://i.imgur.com/v8YXtRj.png)

- ` s.smith : sT333ve2 `
### Gaining Access
![](https://i.imgur.com/4KRPe8i.png)

```shell
rexder@HunterDragon ~/C/H/m/cascade> smbclient -U "cascade.local\s.smith" //10.129.174.190/Audit\$ -c "recurse; ls"
Password for [CASCADE.LOCAL\s.smith]:
  .                                   D        0  Wed Jan 29 21:01:26 2020
  ..                                  D        0  Wed Jan 29 21:01:26 2020
  CascAudit.exe                      An    13312  Wed Jan 29 00:46:51 2020
  CascCrypto.dll                     An    12288  Wed Jan 29 21:00:20 2020
  DB                                  D        0  Wed Jan 29 00:40:59 2020
  RunAudit.bat                        A       45  Wed Jan 29 02:29:47 2020
  System.Data.SQLite.dll              A   363520  Sun Oct 27 09:38:36 2019
  System.Data.SQLite.EF6.dll          A   186880  Sun Oct 27 09:38:38 2019
  x64                                 D        0  Mon Jan 27 01:25:27 2020
  x86                                 D        0  Mon Jan 27 01:25:27 2020

\DB
  .                                   D        0  Wed Jan 29 00:40:59 2020
  ..                                  D        0  Wed Jan 29 00:40:59 2020
  Audit.db                           An    24576  Wed Jan 29 00:39:24 2020

\x64
  .                                   D        0  Mon Jan 27 01:25:27 2020
  ..                                  D        0  Mon Jan 27 01:25:27 2020
  SQLite.Interop.dll                  A  1639936  Sun Oct 27 09:39:20 2019

\x86
  .                                   D        0  Mon Jan 27 01:25:27 2020
  ..                                  D        0  Mon Jan 27 01:25:27 2020
  SQLite.Interop.dll                  A  1246720  Sun Oct 27 09:34:20 2019

		6553343 blocks of size 4096. 1656156 blocks available
```
- We dumped the `Audit.db`
	- ![](https://i.imgur.com/kBHJ9uS.png)
		- `ArkSvc|BQO5l5Kj9MdErXx6Q6AGOw==`
## Internal
### Enumeration
`$enum$`
`C:\Program Files (x86)\WinDirStat\windirstat.exe6..\..\..\Program Files (x86)\WinDirStat\windirstat.exe!C:\Program Files (x86)\WinDirStat`
- tried to check the user we got
	- ![](https://i.imgur.com/hf2tKdP.png)
- ![](https://i.imgur.com/YkxrDZu.png)
- This Executable is on the share so i downloaded it and tried to reverse it
	- ![](https://i.imgur.com/Hy4c5oI.png)
- the `.NET CLR Manged` tells us that this is `.net` program so can be reversed with dnspy or something like that
![](https://i.imgur.com/wtoNihY.png)
![](https://i.imgur.com/5MmpWOZ.png)
- This Library is on the share too
	- ![](https://i.imgur.com/XbvREEZ.png)
- The Function do,
	1. it will decode from base64 
	2. then do AES decryption using the IV and the key is from the 1st screenshot.
	3. Then we did this manually on cyberchef and we got the password
	4. ![](https://i.imgur.com/j7R2YRp.png)
`  ArkSvc : w3lc0meFr31nd `
![](https://i.imgur.com/Izrvj55.png)
![](https://i.imgur.com/H23OqlN.png)
- We Got old User password `YmFDVDNyMWFOMDBkbGVz`
### Gaining Access
- The HTML File we got on the 1st have told us that, the password of the deleted user and the administrator is same.
- The password we got was not working
	- ![](https://i.imgur.com/SpqkD63.png)
- So i thought about that text is encoded and tried to decode in
	- ![](https://i.imgur.com/FTJeeR2.png)
- ![](https://i.imgur.com/2gRLl4B.png)
### Maintaining Access


# Random Notes