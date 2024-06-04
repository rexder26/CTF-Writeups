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
![](https://i.imgur.com/7TZXZAO.png)
![](https://i.imgur.com/S5yDVGt.png)

![](https://i.imgur.com/VjuPDZj.png)
- on main page source
	- Tried parameters But nothing worked.
![](https://i.imgur.com/3ebQLoh.png)
![](https://i.imgur.com/tSPPa6D.png)
```shell
<!-- authentication mode = dolibarr -->
<!-- cookie name used for this session = DOLSESSID_3dfbb778014aaf8a61e81abec91717e6f6438f92 -->
<!-- urlfrom in this session =  -->

<!-- Common footer is not used for login page, this is same than footer but inside login tpl -->
```
- robots.txt
```shell
User-agent: *
Allow: /public/agenda/agendaexport.php
Allow: /public/demo/
Allow: /public/members/new.php
Allow: /index.php
#Allow: /$
Disallow: /
```
- https://www.swascan.com/security-advisory-dolibarr-17-0-0/

```shell
Parameter dolibarr_main_demo must be defined in conf file with value "default login,default pass" to enable the demo entry page
```
### Gaining Access
https://starlabs.sg/advisories/23/23-4198/
- Then when i use `admin:admin` it worked
![](https://i.imgur.com/PKxZDXx.png)
- I created a php rev shell with this - https://www.swascan.com/security-advisory-dolibarr-17-0-0/
	- used `add container/page` feature
- ![](https://i.imgur.com/yequupl.png)
## Internal
### Enumeration
![](https://i.imgur.com/znUdBgb.png)

`htdocs/includes/sabre/sabre/dav/bin/migrateto30.php:33:php {$argv[0]} "mysql:host=localhost;dbname=sabredav" root password`
```
/var/www/html/crm.board.htb/htdocs/admin/system/database.php


-rwsr-xr-x 1 root root 27K Jan 29  2020 /usr/lib/x86_64-linux-gnu/enlightenment/utils/enlightenment_sys (Unknown SUID binary!)
-rwsr-xr-x 1 root root 15K Jan 29  2020 /usr/lib/x86_64-linux-gnu/enlightenment/utils/enlightenment_ckpasswd (Unknown SUID binary!)
-rwsr-xr-x 1 root root 15K Jan 29  2020 /usr/lib/x86_64-linux-gnu/enlightenment/utils/enlightenment_backlight (Unknown SUID binary!)
-rwsr-xr-x 1 root root 15K Jan 29  2020 /usr/lib/x86_64-linux-gnu/enlightenment/modules/cpufreq/linux-gnu-x86_64-0.23.1/freqset (Unknown SUID binary!)

/usr/local/bin/lprsetup.sh


dolibarr_main_db_pass

master.inc.php

/core/filemanagerdol/connectors/php/connector.php
	./website/temp/rexder/website_pages.sql
./admin/system

./core/filemanagerdol/connectors/php
./conf
```
### Gaining Access
- `/var/www/html/crm.board.htb/htdocs/conf`
```shell
$dolibarr_main_db_host='localhost';
$dolibarr_main_db_port='3306';
$dolibarr_main_db_name='dolibarr';
$dolibarr_main_db_prefix='llx_';
$dolibarr_main_db_user='dolibarrowner';
$dolibarr_main_db_pass='serverfun2$2023!!';


// =====================
// This parameter contains name of Dolibarr database.
//
// Examples:
// $dolibarr_main_db_name='dolibarr';
// $dolibarr_main_db_name='mydatabase';
//
$dolibarr_main_db_name='';


// dolibarr_main_db_user
// =====================
// This parameter contains user name used to read and write into Dolibarr database.
//
// Examples:
// $dolibarr_main_db_user='admin';
// $dolibarr_main_db_user='dolibarruser';
//
$dolibarr_main_db_user='';


// dolibarr_main_db_pass
// =====================
// This parameter contains password used to read and write into Dolibarr database.
//
// Examples:
// $dolibarr_main_db_pass='myadminpass';
// $dolibarr_main_db_pass='myuserpassword';
//
$dolibarr_main_db_pass='';
```
- Password Reuse on user `larissa` works Good
- ![](https://i.imgur.com/INzXLgs.png)

![](https://i.imgur.com/NsoBiGp.png)
### Maintaining Access
- from our Linpeas.sh we saw this binary so i googled it and i got this exploit
- ![](https://i.imgur.com/nFeGJvy.png)
- Then Run the Exploit and BOOM WE are root.
# Random Notes