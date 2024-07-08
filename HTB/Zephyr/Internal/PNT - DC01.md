# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
` web_svc : !QAZ1qaz ``
## External
### Enumeration
```
PORT     STATE SERVICE       REASON         VERSION
53/tcp   open  domain        syn-ack ttl 64 Simple DNS Plus
88/tcp   open  kerberos-sec  syn-ack ttl 64 Microsoft Windows Kerberos (server time: 2024-06-27 04:56:11Z)
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
389/tcp  open  ldap          syn-ack ttl 64 Microsoft Windows Active Directory LDAP (Domain: painters.htb0., Site: Default-First-Site-Name)
445/tcp  open  microsoft-ds? syn-ack ttl 64
464/tcp  open  kpasswd5?     syn-ack ttl 64
593/tcp  open  ncacn_http    syn-ack ttl 64 Microsoft Windows RPC over HTTP 1.0
636/tcp  open  tcpwrapped    syn-ack ttl 64
3268/tcp open  ldap          syn-ack ttl 64 Microsoft Windows Active Directory LDAP (Domain: painters.htb0., Site: Default-First-Site-Name)
3269/tcp open  tcpwrapped    syn-ack ttl 64
3389/tcp open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: PAINTERS
|   NetBIOS_Domain_Name: PAINTERS
|   NetBIOS_Computer_Name: DC
|   DNS_Domain_Name: painters.htb
|   DNS_Computer_Name: DC.painters.htb
|   DNS_Tree_Name: painters.htb
|   Product_Version: 10.0.20348
|_  System_Time: 2024-06-27T04:56:26+00:00
|_ssl-date: 2024-06-27T04:57:06+00:00; +5s from scanner time.
| ssl-cert: Subject: commonName=DC.painters.htb
| Issuer: commonName=DC.painters.htb
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-06-25T21:27:13
| Not valid after:  2024-12-25T21:27:13
| MD5:   c6c3:d1b5:cb6a:2319:c8ec:75d1:4ede:01a3
| SHA-1: 560e:6220:8bfe:859d:185d:64b3:fb66:808f:5afe:8285
| -----BEGIN CERTIFICATE-----
| MIIC4jCCAcqgAwIBAgIQMXsKDgsxbrBEPHcyC1ehSTANBgkqhkiG9w0BAQsFADAa
| MRgwFgYDVQQDEw9EQy5wYWludGVycy5odGIwHhcNMjQwNjI1MjEyNzEzWhcNMjQx
| MjI1MjEyNzEzWjAaMRgwFgYDVQQDEw9EQy5wYWludGVycy5odGIwggEiMA0GCSqG
| SIb3DQEBAQUAA4IBDwAwggEKAoIBAQDeux5jYGyuCKljei0HHbKRsXLIa+wVQQWF
| 4qh0G7A85on7NUBf8Bdr29M1ss7QUUWDUgrDhQItV5BI7Ki3ENe/bVflyZJ6xJiM
| 8egEjJK1PP4rfE3PsBYgGLB9euVYyPh8hCugnkMMbIQov8hMk5O0OhZYxXpNapiC
| BVD2AdKE1/JuwIK8vpeGXdqNhJ4I4N5arL7MOTtgbd6o83QBhpnrEI+JdYTIMRCx
| tJfv4fkkJBgGluEJbR0+o/EDXGdR+3A4sHOZQbLLvSHh8KLP3ZR5wfGnLAq1I9vt
| KH7AVBBDmwooX9oS4ZsLQM8FrKC0PMBAD6mWKiCNrhJNz+diYtJtAgMBAAGjJDAi
| MBMGA1UdJQQMMAoGCCsGAQUFBwMBMAsGA1UdDwQEAwIEMDANBgkqhkiG9w0BAQsF
| AAOCAQEAbAOwQabzNe3Wwjh9v877BRXRDt9aM3NVy25L1Rj6vaRYwNHOfRyZN8ln
| ut6FgwLk/Zoc44JoZeR37olobEGG/FHOu518GZeSOhwLEIsR1/1CuEssL9yfUnWS
| zgS8rgZcAF6seI8pfVv7BWRC9Tp9laZdcqa04dB76IWUzAB2PQeDRWx5mjhrvkgT
| QJgX6mRwHK9Rby1ghTyyOW7vL28q/paOyUeXxmVlmiAXkEtRQ/Wgv0Jtom/6M0f9
| eBw1taaZ9mDH8zttejhxScmakNQ3gVFf/KeA4QzK6Zen3TIWflZLdbiGmt1+3LLP
| wwmnRCPKlEsWIb9Rts0AupV46w9N3g==
|_-----END CERTIFICATE-----
Service Info: Host: DC; OS: Windows; CPE: cpe:/o:microsoft:windows

Host script results:
| smb2-security-mode:
|   3:1:1:
|_    Message signing enabled and required
| smb2-time:
|   date: 2024-06-27T04:56:26
|_  start_date: N/A
|_clock-skew: mean: 4s, deviation: 0s, median: 4s
| nbstat: NetBIOS name: DC, NetBIOS user: <unknown>, NetBIOS MAC: 00:50:56:b0:6a:92 (VMware)
| Names:
|   DC<00>               Flags: <unique><active>
|   PAINTERS<00>         Flags: <group><active>
|   PAINTERS<1c>         Flags: <group><active>
|   DC<20>               Flags: <unique><active>
|   PAINTERS<1b>         Flags: <unique><active>
| Statistics:
|   00:50:56:b0:6a:92:00:00:00:00:00:00:00:00:00:00:00
|   00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00:00
|_  00:00:00:00:00:00:00:00:00:00:00:00:00:00
| p2p-conficker:
|   Checking for Conficker.C or higher...
|   Check 1 (port 33990/tcp): CLEAN (Timeout)
|   Check 2 (port 49152/tcp): CLEAN (Timeout)
|   Check 3 (port 8180/udp): CLEAN (Timeout)
|   Check 4 (port 59882/udp): CLEAN (Timeout)
|_  0/4 checks are positive: Host is CLEAN or ports are blocked

Nmap scan report for 192.168.110.55
Host is up, received user-set (0.00088s latency).
Scanned at 2024-06-27 10:49:40 UTC for 231s
Not shown: 65514 filtered ports
Reason: 65514 no-responses
PORT      STATE SERVICE      REASON
53/tcp    open  domain       syn-ack
88/tcp    open  kerberos     syn-ack
135/tcp   open  epmap        syn-ack
139/tcp   open  netbios-ssn  syn-ack
389/tcp   open  ldap         syn-ack
445/tcp   open  microsoft-ds syn-ack
464/tcp   open  kpasswd      syn-ack
593/tcp   open  unknown      syn-ack
636/tcp   open  ldaps        syn-ack
3268/tcp  open  unknown      syn-ack
3269/tcp  open  unknown      syn-ack
5985/tcp  open  unknown      syn-ack
9389/tcp  open  unknown      syn-ack
10050/tcp open  zabbix-agent syn-ack
49664/tcp open  unknown      syn-ack
49667/tcp open  unknown      syn-ack
49669/tcp open  unknown      syn-ack
54540/tcp open  unknown      syn-ack
54549/tcp open  unknown      syn-ack
54553/tcp open  unknown      syn-ack
54563/tcp open  unknown      syn-ack
```
![](https://i.imgur.com/PMfb0Qb.png)

![](https://i.imgur.com/lgpNbNi.png)
- `painters.htb\riley:P@ssw0rd`
- We got Kerberostable accounts
![](https://i.imgur.com/CyWR0ti.png)
- We did KErberosting
![](https://i.imgur.com/qaV5B9Y.png)
![](https://i.imgur.com/B13Aoyh.png)
- ` web_svc : !QAZ1qaz `
- ![](https://i.imgur.com/2AZXEPf.png)
[[PNT - SVRSVC]] 
Domain Compromise obained by [[PNT - SVRBPA]] < - Constrain delegation
- For Come back use this
	- `painters.htb\daniel:b084c663ad3f214e516e6f89c81c80d7`
	- Also for next time dont change the admins password then dump the hash 
- After Domain Compromise i did secretsdump, and i got matts password
![](https://i.imgur.com/sWPiHaR.png)
- `painters.htb\Matt:CLEARTEXT:L1f30f4Spr1ngCh1ck3n!`
	- And We know matt from the linux [[CTF Notes/HTB/Zephyr/External/Foothold]]
### Gaining Access
- I tried to get another COmputers from the DC
```powershell
PS C:\Windows\system32> Import-Module ActiveDirectory
Import-Module ActiveDirectory

PS C:\Windows\system32> $computers = Get-ADComputer -Filter * -Property Name, IPv4Address
$computers = Get-ADComputer -Filter * -Property Name, IPv4Address
```
- I have owned all except the `maintainance`
![](https://i.imgur.com/fYcS7yR.png)
## Internal
### Enumeration
![](https://i.imgur.com/hRIPoxg.png)
```powershell
Get-DomainTrust


SourceName      : painters.htb
TargetName      : zsm.local
TrustType       : WINDOWS_ACTIVE_DIRECTORY
TrustAttributes : FOREST_TRANSITIVE
TrustDirection  : Bidirectional
WhenCreated     : 28/03/2022 08:04:26
WhenChanged     : 27/06/2024 09:43:14
```
- The `ForestTranstive` is True
- Enumerating the Object of the external domain
![](https://i.imgur.com/J6wOA3S.png)
- we got another subnet
![](https://i.imgur.com/rA9yZID.png)
```
riley@mail:~$ seq 1 254 | xargs -P 0 -I {} ping -c 1 -W 1 192.168.210.{} | grep "64 bytes" | awk '{print $4}' | sed 's/://'
192.168.210.1
192.168.210.10
192.168.210.13
192.168.210.16
```
![](https://i.imgur.com/zwC3M7C.png)
[[ZPH - SVRDC01]]
### Gaining Access


### Maintaining Access


# Random Notes