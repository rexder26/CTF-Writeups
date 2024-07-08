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
![](https://i.imgur.com/etLP4ob.png)
![](https://i.imgur.com/WV8A8RF.png)
![](https://i.imgur.com/qAHaKne.png)
![](https://i.imgur.com/dwTFnHz.png)
![](https://i.imgur.com/i5iI1Jd.png)
- i opened it online and got this
	- ![](https://i.imgur.com/x0gpyV0.png)
![](https://i.imgur.com/KW7RZ0X.png)
- When i try it on the zip file it worked. - `"password": "access4u@security"`
	- ![](https://i.imgur.com/m7IjLF7.png)
	- ![](https://i.imgur.com/b5cuMNz.png)
```shell
rexder@HunterMachine ~/C/H/M/access> cat rexder/Access\ Control/mbox
From "john@megacorp.com" Fri Aug 24 02:44:07 2018
Status: RO
From: john@megacorp.com <john@megacorp.com>
Subject: MegaCorp Access Control System "security" account
To: 'security@accesscontrolsystems.com'
Date: Thu, 23 Aug 2018 23:44:07 +0000
MIME-Version: 1.0
Content-Type: multipart/mixed;

Hi there,

The password for the “security” account has been changed to 4Cc3ssC0ntr0ller.  Please ensure this is passed on to your engineers.



Regards,

John

--alt---boundary-LibPST-iamunique-1855378941_-_---

----boundary-LibPST-iamunique-1855378941_-_---
```
### Gaining Access
` security : 4Cc3ssC0ntr0ller `![](https://i.imgur.com/6h9zMv3.png)

## Internal
### Enumeration
```
    <add name="Access.Properties.Settings.ZKAccessConnectionString" connectionString="Provider=Microsoft.Jet.OLEDB.4.0;Persist Security Info=true;Jet OLEDB:Database Password=pwd;Data Source=|DataDirectory|\ZKAccess.mdb" providerName="System.Data.OleDb"/>
```

### Gaining Access


### Maintaining Access
![](https://i.imgur.com/oJBNTVX.png)
![](https://i.imgur.com/H6xt0Fe.jpeg)


# Random Notes