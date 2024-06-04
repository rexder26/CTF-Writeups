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
![](https://i.imgur.com/AZBsjQk.png)
![](https://i.imgur.com/3YR0lqR.png)
![](https://i.imgur.com/Kkq2PbP.png)
https://github.com/amriunix/ona-rce?tab=readme-ov-file
![](https://i.imgur.com/UT342tk.png)
### Gaining Access
```shell
(remote) www-data@openadmin:/opt/ona$ ss -lntp
State                          Recv-Q                          Send-Q                                                     Local Address:Port                                                      Peer Address:Port
LISTEN                         0                               80                                                             127.0.0.1:3306                                                           0.0.0.0:*
LISTEN                         0                               128                                                            127.0.0.1:52846                                                          0.0.0.0:*
LISTEN                         0                               128                                                        127.0.0.53%lo:53                                                             0.0.0.0:*
LISTEN                         0                               128                                                              0.0.0.0:22                                                             0.0.0.0:*
LISTEN                         0                               128                                                                    *:80                                                                   *:*
LISTEN                         0                               128                                                                 [::]:22                                                                [::]:*
include/adodb5/adodb-pear.inc.php:257:	 *  phptype://username:password@protocol+hostspec:110//usr/db_file.db
/opt/ona/www/config/auth_ldap.config.php
/opt/ona/www/local/config/database_settings.inc.php

/var/www/html/marga/.git/
/opt/ona/www/login.php

/local/config/database_settings.inc.php
```
`mysecretbindpassword`
## Internal
### Enumeration
![](https://i.imgur.com/Tdr2sLA.png)
```shell
     'db_login' => 'ona_sys',
        'db_passwd' => 'n1nj4W4rri0R!',
        'db_database' => 'ona_default',
        'db_debug' => false,

+----+----------+----------------------------------+-------+---------------------+---------------------+
| id | username | password                         | level | ctime               | atime               |
+----+----------+----------------------------------+-------+---------------------+---------------------+
|  1 | guest    | 098f6bcd4621d373cade4e832627b4f6  -> test |     0 | 2024-06-03 20:12:14 | 2024-06-03 20:12:14 |
|  2 | admin    | 21232f297a57a5a743894a0e4a801fc3 -> admin |     0 | 2024-06-03 14:53:01 | 2024-06-03 14:53:01 |
+----+----------+----------------------------------+-------+---------------------+---------------------+

drwxr-x---  6 jimmy  jimmy  4096 Jun  3 18:17 jimmy
drwxr-x---  5 joanna joanna 4096 Jul 27  2021 joanna
```
### Gaining Access
- password reuse
- ![](https://i.imgur.com/5QGl5ZY.png)
![](https://i.imgur.com/Q1NP5Ki.png)

![](https://i.imgur.com/8fZnmjH.jpeg)
![](https://i.imgur.com/b0l3ueh.png)
![](https://i.imgur.com/EOsEOvl.png)
### Maintaining Access

![](https://i.imgur.com/oqHU3QS.png)

![](https://i.imgur.com/99M7bu9.png)


# Random Notes