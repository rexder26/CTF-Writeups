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
![](https://i.imgur.com/ki5z3Bd.png)
![](https://i.imgur.com/VMcQuh5.png)
![](https://i.imgur.com/GDvBR7v.png)
![](https://i.imgur.com/FQZb8ME.png)
![](https://i.imgur.com/ShRC9OL.png)
![](https://i.imgur.com/5hvVopE.png)
- [John Doe](http://shibboleth.htb/blog-single.html)
![](https://i.imgur.com/6w8KVYy.png)
https://book.hacktricks.xyz/network-services-pentesting/623-udp-ipmi
![](https://i.imgur.com/4UQzFZg.png)
![](https://i.imgur.com/sFudIjN.png)
`Administrator:09a779ef8204000064082bb9d4ba7fddf22ae79700a59a93e6b4549a2b660fc37d29fbe27cca893ea123456789abcdefa123456789abcdef140d41646d696e6973747261746f72:d18f8a89b40799ced89a62d3c98e55613dd51000`
![](https://i.imgur.com/6SpUGW7.png)
hashcat -m 7300 hash /usr/share/wordlists/rockyou.txt
![](https://i.imgur.com/dJ9PaO2.png)
- ` Administrator : ilovepumkinpie1 `
### Gaining Access
![](https://i.imgur.com/4d0RFNR.jpeg)
https://www.exploit-db.com/exploits/50816
![](https://i.imgur.com/kcRJcLE.png)
![](https://i.imgur.com/zsInmZp.png)
## Internal
### Enumeration
Sudo version 1.8.31
![](https://i.imgur.com/nXszdze.png)
/var/www/html
### Gaining Access
- password re use worked!
- ![](https://i.imgur.com/LQgCGIU.png)/var/lib/mysql
- /etc/zabbix/zabbix_server.conf
- /etc/mysql/mariadb.conf.d/50-server.cnf
- /zabbix/api_jsonrpc.php
![](https://i.imgur.com/uw0TL4r.png)
```
SocketDir=/run/zabbix
DBName=zabbix
DBUser=zabbix
DBPassword=bloooarskybluh
```
![](https://i.imgur.com/OtdDQdy.png)

### Maintaining Access
![](https://i.imgur.com/LqQbYnP.png)
![](https://i.imgur.com/UT3UJ4X.png)
https://github.com/Al1ex/CVE-2021-27928

# Random Notes