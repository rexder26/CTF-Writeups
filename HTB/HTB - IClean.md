# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #xss #ssti #jinja #qpdf

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
```
about                   [Status: 200, Size: 5267, Words: 1036, Lines: 130, Duration: 458ms]
dashboard               [Status: 302, Size: 189, Words: 18, Lines: 6, Duration: 433ms]
login                   [Status: 200, Size: 2106, Words: 297, Lines: 88, Duration: 441ms]
logout                  [Status: 302, Size: 189, Words: 18, Lines: 6, Duration: 446ms]
quote                   [Status: 200, Size: 2237, Words: 98, Lines: 90, Duration: 484ms]
server-status           [Status: 403, Size: 278, Words: 20, Lines: 10, Duration: 570ms]
services                [Status: 200, Size: 8592, Words: 2325, Lines: 193, Duration: 574ms]
team                    [Status: 200, Size: 8109, Words: 2068, Lines: 183, Duration: 434ms]
choose                  [Status: 200, Size: 6084, Words: 1373, Lines: 154, Duration: 428ms]

```
- There is an endpoint `/sendMessage` and i will send a service list to the cleaners management team
	- ![](https://i.imgur.com/1muKvC9.png)
- so what i thought was, then if i send some xss link if they open it i will get their cookie, so tried it with simple payload.
	- ![](https://i.imgur.com/E01Z4n2.png)
	- ![](https://i.imgur.com/ThSaGKH.png)
- Therefore, I can use the cookie stealing.
	- ![](https://i.imgur.com/G5H0Jr8.png)

	- ![](https://i.imgur.com/zfR0o8O.png)
- we got admin
	- ![](https://i.imgur.com/WVBl11v.png)
`session=eyJyb2xlIjoiMjEyMzJmMjk3YTU3YTVhNzQzODk0YTBlNGE4MDFmYzMifQ.Zhy40A.jKLPMVe81GJWKA5h7zrwY5RaFZI`
 - On the below page, you can Generate invoice code with the parameters listed. and you can generate qr code of invoice page using the code that gives you.
	 - `http://capiclean.htb/InvoiceGenerator`![](https://i.imgur.com/hpcRSAV.png)
	- `http://capiclean.htb/QRGenerator`![](https://i.imgur.com/eDSMxjg.png)
- Finally, when you scan the qr code that gives you it will lead to
	- ![](https://i.imgur.com/IakpMRx.png)
- As you see the client,Project, address names you give on the invoice generate will be displaied here, so i was trying to do some `SSTI` and unfortunately i cant bypass with any encoding. but i checked that, except the quality number we give ever other thing is JS random generated. when you refresh the page it changes. so i tried to check the `4000` quality.
	- Tried But failed, i think i have to get better payload than `{7*7}` and good encoding.
		- ![](https://i.imgur.com/8FypSdJ.png)
- After some tries of encoding, i stopped that and tried to get another path.
	- ![](https://i.imgur.com/I30r0Xt.png)
- i got XSS on the page, Then I tried SSTI.
	- ![](https://i.imgur.com/22zUM5W.png)
- BOOOM! it worked!
- Started enumerating the jinja
	- ![[Pasted image 20240415104320.png]]![](https://i.imgur.com/2HA5e9O.png)
	![](https://i.imgur.com/nYM8aEI.png)
`'SECRET_KEY': 'mtuwhnmewthbculnynzirhnqhpveztaamemrhivaknxdkoxfrutdmvdonqkgyycy'`
- Everything was working but when i continue with some syntaxs it is saying 500
	- ![](https://i.imgur.com/LwzuNl1.png)
- So i tried to encode with url but not workin, then tried HEx and it worked!
	- ![](https://i.imgur.com/Uof1BVy.png)
- {{["YOURPAYLOAD"]}} - but i have to fix it a lil bit
	- ![](https://i.imgur.com/SN81MBr.png)
- https://www.onsecurity.io/blog/server-side-template-injection-with-jinja2/ 
![](https://i.imgur.com/TyMOnMS.png)
- RCE is here!

![](https://i.imgur.com/jaTClBz.png)
![](https://i.imgur.com/u9tXE91.png)
![](https://i.imgur.com/VQ2ljIk.png)
![](https://i.imgur.com/m7THhEy.png)
![](https://i.imgur.com/WyBUaib.png)- mysql is running on different ports, we just need credentials...lets check config files.
	![](https://i.imgur.com/7lrpy9Q.png)
- we got config in `app.py`
	- ![](https://i.imgur.com/eA8qWMg.png)
```shell
 'user': 'iclean',
    'password': 'pxCsmnGLckUb',
    'database': 'capiclean'
```
![](https://i.imgur.com/UIbYH75.png)
![](https://i.imgur.com/Q9Zu5tw.png)
![](https://i.imgur.com/PcShoXS.png)
`consuela : simple and clean`
- we got ssh
![](https://i.imgur.com/o4UMUoI.png)
![](https://i.imgur.com/A4p8rr8.png)
![](https://i.imgur.com/7l3K3Si.png)
![](https://i.imgur.com/PLDHKqr.png)
![](https://i.imgur.com/PEx1XHp.png)

https://stackoverflow.com/questions/11731425/data-extraction-from-filter-flatedecode-pdf-stream-in-php
![](https://i.imgur.com/JHQCSiq.png)
