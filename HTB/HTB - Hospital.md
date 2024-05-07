# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #fileUpload #GhostScript #mail

# Findings

## External
### Enumeration
`$enum$`

### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes
![](https://i.imgur.com/4SPN2Vb.png)
- KErberos is on
- Ldap is on
- RPC is on
- RDP is on
- 5985
![](https://i.imgur.com/HdKwgjy.png)
![](https://i.imgur.com/SPnkulg.png)
![](https://i.imgur.com/EwItRuW.png)
![](https://i.imgur.com/3F4UhkX.png)

![](https://i.imgur.com/aBOTqds.png)
- ![](https://i.imgur.com/Y1CVM1P.png)

Thee is upload Directory
- We got the File but the code is not excuteing
	- ![](https://i.imgur.com/7rPjNIK.png)
	- So lets Change the rev shell code.
		- ![](https://i.imgur.com/DmZqOek.png)
	- We are getting shell and Disconnecting, with revshell.
		- Webshell is not working too.
		- After some help from the community
			- ![](https://i.imgur.com/XGTe4XN.png)
- we uploaded https://github.com/flozz/p0wny-shell/blob/master/shell.php
- We got Access to linux machine
	- ![](https://i.imgur.com/Ks4Zxf7.png)
- we got User - `drwilliams`
- ![](https://i.imgur.com/GAOQ56d.png)
We got shell on our machine
![](https://i.imgur.com/yRzVK5B.png)
- we got creds
	- ![](https://i.imgur.com/GI6eHu1.png)
- `root : my$qls3rv1c3!`
- ![](https://i.imgur.com/hUJcm49.png)
![](https://i.imgur.com/WtfyDGZ.png)
from admin and a
- My Privilege escalating [tool](https://github.com/g1vi/CVE-2023-2640-CVE-2023-32629?source=post_page-----ce86940a895f--------------------------------)

![](https://i.imgur.com/czOcMwm.png)
![](https://i.imgur.com/YEJZXtx.png)
- `drwilliams : qwe123!@#`
- `drbrown : chr!$br0wn`
- `cfgsmtpuseru : `
```
Dear Lucy,  
  
I wanted to remind you that the project for lighter, cheaper and  
environmentally friendly needles is still ongoing 💉. You are the one in  
charge of providing me with the designs for these so that I can take  
them to the 3D printing department and start producing them right away.  
Please make the design in an ".eps" file format so that it can be well  
visualized with GhostScript.  
  
Best regards,  
Chris Brown.  
😃
```
![](https://i.imgur.com/jFHktPZ.png)
- Logged in with the drwilliams credentials
- ![](https://i.imgur.com/vdScmU3.png)
https://github.com/duc-nt/RCE-0-day-for-GhostScript-9.50
- Tried to upload the paylod with certutil and it is not working
	- ![](https://i.imgur.com/Aug2cfw.png)
- Lets Try another.
	- ![](https://i.imgur.com/pYoRvf2.png)
 after so many tool change it worked.

after 6 hours of try finally it worked
	![](https://i.imgur.com/n6y63Bn.png)
![](https://i.imgur.com/RhgEELJ.png)
- I got password of drbrown
- ![](https://i.imgur.com/1yO9a4Z.png)
- User.txt
	- ![](https://i.imgur.com/RaazKAY.png)
C:\xampp\phpMyAdmin\config.inc.php
C:\xampp\htdocs\installer\config.php
```shell
$input_dbhost = new html_inputfield(['name' => '_dbhost', 'size' => 20, 'id' => 'cfgdbhos']);
$input_dbuser = new html_inputfield(['name' => '_dbuser', 'size' => 20, 'id' => 'cfgdbuser']);
$input_dbpass = new html_inputfield(['name' => '_dbpass', 'size' => 20, 'id' => 'cfgdbpass']);
```

![](https://i.imgur.com/24odchl.png)
![](https://i.imgur.com/mtAXVJT.png)
![](https://i.imgur.com/GwqCHsD.png)
