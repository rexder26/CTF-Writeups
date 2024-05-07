# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #activedirectory #PAC #mssql

# Findings

## External
### Enumeration
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240430225557.png]]
![](https://i.imgur.com/xZf8piM.png)
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240501115633.png]]
![](https://i.imgur.com/CFttM14.png)
![](https://i.imgur.com/5rnmBoE.png)
![](https://i.imgur.com/M2OebTO.png)

![](https://i.imgur.com/oonoUib.png)
![](https://i.imgur.com/gtentcE.png)
- Nothing Over here. - i think it is rabbit hole
![](https://i.imgur.com/pjBjzwJ.png)
![](https://i.imgur.com/EnjoTJE.png)
![](https://i.imgur.com/rDiWVSX.png)
![](https://i.imgur.com/wySibwY.png)
![](https://i.imgur.com/mDAVsFm.png)
![](https://i.imgur.com/xdp1BXk.png)
![](https://i.imgur.com/NpMhI71.png)
- But not working, then i realized there is a random letter on the file name `dev_notes_random..` so that can be password, but it is not then i thought about hash, so i put it on cyberchef and it worked.
- ![](https://i.imgur.com/j0irq06.png)
` admin : m$$ql_S@_P@ssW0rd! `

### Gaining Access
![](https://i.imgur.com/xNpL7UI.png)
![](https://i.imgur.com/fBDxyuY.png)
- the ntlmv2 was not crackable
- so i tried to get users and impersonate and run some commands
	- ![](https://i.imgur.com/8JAcKrq.png)
- I tried to check the permissions i have, and i just do viewing 
	- ![](https://i.imgur.com/znEW4oC.png)

- Then Try to check if there is any thing savvy
	- ![](https://i.imgur.com/0AOQVq9.png)

- I got user data, with password for use james
	- ![](https://i.imgur.com/O3gZvIA.png)
	- ` james : J@m3s_P@ssW0rd! `
## Internal
### Enumeration
- The user we got is a domain user
	- ![](https://i.imgur.com/spwMznE.png)
### Gaining Access
The user is part of the "Remote Desktop Users" group, however, no RDP ports are open. We have no WinRM and not enough privileges to gain code execution through the use of psexec,wmiexec and so forth...

At this point I ran extra vulnerability scans against the target with Nmap and Nessus and still, nothing...
![](https://i.imgur.com/s0BOnLl.png)
- if there is a delay between the DC we can exploit
### Maintaining Access
![](https://i.imgur.com/83BkmKZ.png)
# Random Notes