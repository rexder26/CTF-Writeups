# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
`FoundCREDs`
## External
### Enumeration
![](https://i.imgur.com/unoi8ip.png)
https://exploit-notes.hdks.org/exploit/web/icinga-web-pentesting/
https://www.exploit-db.com/exploits/51329
```shell
[global]
show_stacktraces = "1"
show_application_state_messages = "1"
config_backend = "db"
config_resource = "icingaweb2"
module_path = "/usr/share/icingaweb2/modules/"

[logging]
log = "syslog"
level = "ERROR"
application = "icingaweb2"
facility = "user"

[themes]

[authentication]

[icingaweb2]
type = "db"
db = "mysql"
host = "localhost"
dbname = "icingaweb2"
username = "matthew"
password = "IcingaWebPassword2023"
use_ssl = "0"
```

### Gaining Access
![](https://i.imgur.com/aNgiobm.png)
![](https://i.imgur.com/sK77Vn7.png)
## Internal
### Enumeration
![](https://i.imgur.com/7Chiq5b.png)
![](https://i.imgur.com/Qt0BVvN.png)
![](https://i.imgur.com/CJvP7q8.png)
This linux box was in a domain connected to DC, so i made the linux jump host using ligolo
```shell
rexder@HunterMachine ~/C/H/M/cerberus [1]> fping -asgq 172.16.22.0/24
172.16.22.1
172.16.22.2
```
![](https://i.imgur.com/LdQGr6j.png)
https://gist.github.com/GugSaas/9fb3e59b3226e8073b3f8692859f8d25
### Gaining Access
![](https://i.imgur.com/2v0QXGt.png)
![](https://i.imgur.com/DPEgPKH.png)
![](https://i.imgur.com/chltxqT.png)
![](https://i.imgur.com/ptPY3qo.png)
` matthew : 147258369`
![](https://i.imgur.com/J74vj48.png)
### Maintaining Access
![](https://i.imgur.com/A6EGiJn.png)
![](https://i.imgur.com/MK60MRe.png)
- when i see open ports there is on different port. and it looks web page
![](https://i.imgur.com/SUby34m.png)
- also the payload needs web page there for this might be
![](https://i.imgur.com/kaMvIPP.png)



# Random Notes