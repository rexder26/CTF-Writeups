# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `172.16.1.5`

# Findings
### Credentials
`FoundCREDs`

### Flags
1. `DANTE{Ther3s_M0r3_to_pwn_so_k33p_searching!}`
2. `DANTE{Mult1ple_w4Ys_in!}`
3. `DANTE{Ju1cy_pot4t03s_in_th3_wild}`
## External
### Enumeration
```shell
# Nmap 7.94SVN scan initiated Sat Jun 22 11:04:13 2024 as: nmap -v -sCV -oN Scan_Results/all.nmap 172.16.1.20,5,19,10,12,17,13,101,102
Nmap scan report for 172.16.1.5
Host is up (0.18s latency).
Not shown: 993 closed tcp ports (reset)
PORT     STATE SERVICE      VERSION
21/tcp   open  ftp          FileZilla ftpd
| ftp-anon: Anonymous FTP login allowed (FTP code 230)
|_-r--r--r-- 1 ftp ftp             44 Jan 08  2021 flag.txt
| ftp-syst: 
|_  SYST: UNIX emulated by FileZilla
111/tcp  open  rpcbind      2-4 (RPC #100000)
| rpcinfo: 
|   program version    port/proto  service
|   100000  2,3,4        111/tcp   rpcbind
|   100000  2,3,4        111/tcp6  rpcbind
|   100000  2,3,4        111/udp   rpcbind
|   100000  2,3,4        111/udp6  rpcbind
|   100003  2,3         2049/udp   nfs
|   100003  2,3         2049/udp6  nfs
|   100003  2,3,4       2049/tcp   nfs
|   100003  2,3,4       2049/tcp6  nfs
|   100005  1,2,3       2049/tcp   mountd
|   100005  1,2,3       2049/tcp6  mountd
|   100005  1,2,3       2049/udp   mountd
|   100005  1,2,3       2049/udp6  mountd
|   100021  1,2,3,4     2049/tcp   nlockmgr
|   100021  1,2,3,4     2049/tcp6  nlockmgr
|   100021  1,2,3,4     2049/udp   nlockmgr
|   100021  1,2,3,4     2049/udp6  nlockmgr
|   100024  1           2049/tcp   status
|   100024  1           2049/tcp6  status
|   100024  1           2049/udp   status
|_  100024  1           2049/udp6  status
135/tcp  open  msrpc        Microsoft Windows RPC
139/tcp  open  netbios-ssn  Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1433/tcp open  ms-sql-s     Microsoft SQL Server 2019 15.00.2000.00; RTM
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-06-22T03:15:23
| Not valid after:  2054-06-22T03:15:23
| MD5:   27b3:aaad:42cb:7f83:0f25:fa8b:2d43:bf4d
|_SHA-1: bb73:c528:ef0f:9a6c:4695:7390:7d3a:ce7c:34ae:976e
| ms-sql-ntlm-info: 
|   172.16.1.5\SQLEXPRESS: 
|     Target_Name: DANTE-SQL01
|     NetBIOS_Domain_Name: DANTE-SQL01
|     NetBIOS_Computer_Name: DANTE-SQL01
|     DNS_Domain_Name: DANTE-SQL01
|     DNS_Computer_Name: DANTE-SQL01
|_    Product_Version: 10.0.14393
|_ssl-date: 2024-06-22T08:09:30+00:00; +1s from scanner time.
| ms-sql-info: 
|   172.16.1.5\SQLEXPRESS: 
|     Instance name: SQLEXPRESS
|     Version: 
|       name: Microsoft SQL Server 2019 RTM
|       number: 15.00.2000.00
|       Product: Microsoft SQL Server 2019
|       Service pack level: RTM
|       Post-SP patches applied: false
|     TCP port: 1433
|_    Clustered: false
2049/tcp open  nlockmgr     1-4 (RPC #100021)
Service Info: OSs: Windows, Windows Server 2008 R2 - 2012; CPE: cpe:/o:microsoft:windows
47001/tcp
```
![](https://i.imgur.com/O1ad6Za.png)

![](https://i.imgur.com/qs2wSz7.png)
- Tried windows exploit they were not working.
Using the creds from [[Dante - NIX06]]
	- ` sophie : TerrorInflictPurpleDirt996655` 
### Gaining Access
![](https://i.imgur.com/M2YT2aV.png)
![](https://i.imgur.com/dIJ3BKz.png)

## Internal
### Enumeration
![](https://i.imgur.com/RjyU62y.png)
![](https://i.imgur.com/PzVWbo6.png)

### Gaining Access

### Maintaining Access
![](https://i.imgur.com/HJodOtF.png)


# Random Notes
