# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #openssl 

# Findings

## External
### Enumeration
![](https://i.imgur.com/J7ndQ04.png)
![](https://i.imgur.com/0Kse7Kl.png)
![](https://i.imgur.com/fAsR7Oa.png)
![](https://i.imgur.com/5gEdF6C.png)
![](https://i.imgur.com/eTUx4to.png)
- https://github.com/glv2/bruteforce-salted-openssl
	- or `apt install bruteforce-salted-openssl`
- ![](https://i.imgur.com/vRRQcQS.png)
` friends `
![](https://i.imgur.com/08YKelt.png)
- Drupal Login: ` drupal : PencilKeyboardScanner123 `
![](https://i.imgur.com/RQzPGXu.png)

![](https://i.imgur.com/v6NRTHv.png)
```
# Dirs
0                       [Status: 200, Size: 7384, Words: 805, Lines: 157, Duration: 255ms]
LICENSE                 [Status: 200, Size: 18092, Words: 3133, Lines: 340, Duration: 168ms]
README                  [Status: 200, Size: 5382, Words: 684, Lines: 124, Duration: 142ms]
includes                [Status: 301, Size: 307, Words: 20, Lines: 10, Duration: 219ms]
index.php               [Status: 200, Size: 7384, Words: 805, Lines: 157, Duration: 461ms]
misc                    [Status: 301, Size: 303, Words: 20, Lines: 10, Duration: 165ms]
modules                 [Status: 301, Size: 306, Words: 20, Lines: 10, Duration: 140ms]
node                    [Status: 200, Size: 7384, Words: 805, Lines: 157, Duration: 480ms]
profiles                [Status: 301, Size: 307, Words: 20, Lines: 10, Duration: 211ms]
robots.txt              [Status: 200, Size: 2189, Words: 158, Lines: 91, Duration: 232ms]
robots                  [Status: 200, Size: 2189, Words: 158, Lines: 91, Duration: 237ms]
scripts                 [Status: 301, Size: 306, Words: 20, Lines: 10, Duration: 304ms]
sites                   [Status: 301, Size: 304, Words: 20, Lines: 10, Duration: 214ms]
themes                  [Status: 301, Size: 305, Words: 20, Lines: 10, Duration: 168ms]
user                    [Status: 200, Size: 7217, Words: 755, Lines: 150, Duration: 560ms]
web.config              [Status: 200, Size: 2200, Words: 416, Lines: 47, Duration: 162ms]
xmlrpc.php              [Status: 200, Size: 42, Words: 6, Lines: 1, Duration: 488ms]
```
https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/h2-java-sql-database
![](https://i.imgur.com/2jI6T1f.png)
### Gaining Access
![](https://i.imgur.com/7kb5tUL.png)
- https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/drupal/drupal-rce
![](https://i.imgur.com/F9g9t1i.png)
![](https://i.imgur.com/Yjgo4Ht.png)
`/var/www/html/sites/default/settings.php`
![](https://i.imgur.com/m1oDLMN.png)
`drupal4hawk`
## Internal
### Enumeration
`$enum$`

### Gaining Access
- Password Reuse on `daniel`
- ![](https://i.imgur.com/IFRJrHM.png)
- ![](https://i.imgur.com/JJ8G8Oz.png)


### Maintaining Access
![](https://i.imgur.com/NedsqtA.png)

<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240509205016.png]]
https://mthbernardes.github.io/rce/2018/03/14/abusing-h2-database-alias.html
![](https://i.imgur.com/fOttSMb.png)



# Random Notes
 - Potential Password at /var/www/html/scripts/password-hash.sh
 - includes/database
 - INSTALL.txt
 - sites/default/settings.php - **dsa**
```

'database' => 'drupal',
      'username' => 'drupal',
      'password' => 'drupal4hawk',
  $drupal_hash_salt = 'LrDo0zR-UKwhAUPsDYm5qD-RaI-Llu5kJM8XLF8ZYpg';
  ```
```
:q!
|2,0,1715272872,,"q!"
:!sh
|2,0,1715272867,,"!sh"
:q
|2,0,1528795854,,"q"
:!/bin/sh
|2,0,1528795816,,"!/bin/sh"
:shell
|2,0,1528795806,,"shell"
:set shell=/bin/sh
|2,0,1528795804,,"set shell=/bin/sh"
:SHELL=/bin/bash
|2,0,1528795792,,"SHELL=/bin/bash"
:shell=/bin/bash
|2,0,1528795784,,"shell=/bin/bash"
```