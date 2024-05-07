# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #xss #OSinjection #sudo 

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
![](https://i.imgur.com/0i5Mh6w.png)
- check injection attacks/
```shell
PORT     STATE SERVICE REASON  VERSION
5000/tcp open  upnp?   syn-ack
| fingerprint-strings: 
|   GetRequest: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/2.2.2 Python/3.11.2
|     Date: Tue, 09 Apr 2024 19:55:30 GMT
|     Content-Type: text/html; charset=utf-8
|     Content-Length: 2799
|     Set-Cookie: is_admin=InVzZXIi.uAlmXlTvm8vyihjNaPDWnvB_Zfs; Path=/
|     Connection: close
|   HTTPOptions: 
|     HTTP/1.1 200 OK
|     Server: Werkzeug/2.2.2 Python/3.11.2
|     Date: Tue, 09 Apr 2024 19:55:53 GMT
|     Content-Type: text/html; charset=utf-8
|     Allow: OPTIONS, GET, HEAD
|     Content-Length: 0
|     Connection: close
|   Help: 
|     <!DOCTYPE HTML>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request syntax ('HELP').</p>
|     <p>Error code explanation: 400 - Bad request syntax or unsupported method.</p>
|     </body>
|     </html>
|   RTSPRequest: 
|     <!DOCTYPE HTML>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request version ('RTSP/1.0').</p>
|     <p>Error code explanation: 400 - Bad request syntax or unsupported method.</p>
|     </body>
|     </html>
|   SSLSessionReq: 
|     <!DOCTYPE HTML>
|     <html lang="en">
|     <head>
|     <meta charset="utf-8">
|     <title>Error response</title>
|     </head>
|     <body>
|     <h1>Error response</h1>
|     <p>Error code: 400</p>
|     <p>Message: Bad request syntax ('
|     &lt;=
|     ').</p>
|     <p>Error code explanation: 400 - Bad request syntax or unsupported method.</p>
|     </body>
|_    </html>
```
![](https://i.imgur.com/r5mXIEa.png)
- When i try XSS payloads
	- ![](https://i.imgur.com/2pWEBlU.png)
![](https://i.imgur.com/AkASjLu.png)
- The headless browser accessed my XSS
![](https://i.imgur.com/3bkci8P.png)
![](https://i.imgur.com/JaKGWAF.png)
`is_admin=ImFkbWluIg.dmzDkZNEm6CK0oyL1fbM-SnXpH0`
- The site is about website health, so i though how we can check website health and we might use commands,. so i tried command injection and boom!
- ![](https://i.imgur.com/2c5t0dX.png)
- Reverse shell
	- ![](https://i.imgur.com/GAmqWnY.png)
![](https://i.imgur.com/05bgOUP.png)

# priv
- [ ] check cron
- [ ] /home/dvir/app/app.py
- [ ] /usr/bin/syscheck as ALL on local (NOPASSWD) - sudo -l
![](https://i.imgur.com/j7GMy3R.png)

![](https://i.imgur.com/UJ8eFVf.png)

https://medium.com/@adiamond186/usr-bin-syscheck-is-looking-for-the-initdb-sh-609cd006d913
- created this file
- ![](https://i.imgur.com/lcKQ2Sw.png)

![](https://i.imgur.com/O5necQp.png)
