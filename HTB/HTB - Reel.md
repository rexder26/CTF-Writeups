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
![](https://i.imgur.com/f1DvqAI.png)
445 and 593 are open
![](https://i.imgur.com/2XXrsG2.png)

![](https://i.imgur.com/h6OpTKj.png)
![](https://i.imgur.com/lDJ7eU2.png)
![](https://i.imgur.com/jFqKKRO.png)
- checking metadata f the "Windows Event Forwarding" file
	- ![](https://i.imgur.com/GHUjDQ3.png)
	- `nico@megabank.com`
- <!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240429214338.png]]
	Verified that the user exists.
- We can Email him, Malware so, as he said when he try to open it we will get pingback. For that we need RTF exploit.
	- ![](https://i.imgur.com/2S7K94C.png)https://www.exploit-db.com/exploits/41894
![](https://i.imgur.com/hwQ2mpM.png)
![](https://i.imgur.com/SiLy3OH.png)
![](https://i.imgur.com/TGsMuSD.png)
- ### Gaining Access
![](https://i.imgur.com/fEBa7y1.png)
- ![](https://i.imgur.com/T8EDygR.png)
- ![](https://i.imgur.com/2UNOKza.png)

## Internal
### Enumeration
![](https://i.imgur.com/mwTevJ0.png)
![](https://i.imgur.com/1je5OaM.png)
- Reversed the Password.
![](https://i.imgur.com/v4UDOsw.png)
- Now we have Full Credential
	- `tom : 1ts-mag1c!!! `
- ![](https://i.imgur.com/WrUR6Ax.png)
### Gaining Access
- SSH to the user
	- ![](https://i.imgur.com/xg3pX4w.png)
- I enumerated the domain admins.
![](https://i.imgur.com/1yTwiBh.png)
- I tried to enumerate the `tom` user
![](https://i.imgur.com/feX48zB.png)
![](https://i.imgur.com/zxDjpVi.png)
![](https://i.imgur.com/n98fZLa.png)

### Maintaining Access
![](https://i.imgur.com/Bvo3v5b.png)
![](https://i.imgur.com/RJmGyuT.png)
![](https://i.imgur.com/yZaueyK.png)


# Random Notes