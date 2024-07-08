# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: 

# Findings
### Credentials
- admin - `543beb20a2a579c7714ced68a1760d5e`

### flags
- `ZEPHYR{In73rn4l_D0m41n_D0m1n473d}`
## External
### Enumeration
```
PORT     STATE SERVICE          REASON
53/tcp   open  domain           syn-ack ttl 64
88/tcp   open  kerberos-sec     syn-ack ttl 64
135/tcp  open  msrpc            syn-ack ttl 64
139/tcp  open  netbios-ssn      syn-ack ttl 64
389/tcp  open  ldap             syn-ack ttl 64
445/tcp  open  microsoft-ds     syn-ack ttl 64
464/tcp  open  kpasswd5         syn-ack ttl 64
636/tcp  open  ldapssl          syn-ack ttl 64
3268/tcp open  globalcatLDAP    syn-ack ttl 64
3269/tcp open  globalcatLDAPssl syn-ack ttl 64
```
- users
```shell
2024/06/28 10:34:30 >  [+] VALID USERNAME:	 matt@INTERNAL.ZSM.LOCAL
2024/06/28 10:34:30 >  [+] VALID USERNAME:	 jamie@INTERNAL.ZSM.LOCAL
```
- Matt exists here this means i can use his password or hash?... try it
- ` mssql_svc      ToughPasswordToCrack123! `
![](https://i.imgur.com/1RcFPfX.png)
![](https://i.imgur.com/mSyFgUF.png)
- ` aron : ToughPasswordToCrack123! `
- `SMB         192.168.210.16  445    ZPH-SVRCDC01     [+] .\Aron:ToughPasswordToCrack123!`
```powershell
PS C:\> Get-NetComputer -Domain internal.zsm.local | Select-Object Name, IPv4Address
Get-NetComputer -Domain internal.zsm.local | Select-Object Name, IPv4Address

name          IPv4Address
----          -----------
ZPH-SVRCDC01
ZPH-SVRCHR
ZPH-SVRCSUP
ZSM-SVRCSQL02
INT-MAINT
```
![](https://i.imgur.com/O6DD3wh.png)
- This mens, Aron from the internal domain is memeber of administrators in the zsm.local
[[ZPH - SVRDC01]]
![](https://i.imgur.com/buqxcdU.png)
![](https://i.imgur.com/hLWkU5V.png)
### Gaining Access
![](https://i.imgur.com/Raqhuzd.png)
## Internal
### Enumeration
```shell
PS C:\users> Get-ADComputer -Filter * -Property Name, IPv4Address | select IPv4Address,SamAccountName
Get-ADComputer -Filter * -Property Name, IPv4Address | select IPv4Address,SamAccountName

IPv4Address     SamAccountName
-----------     --------------
192.168.210.16  ZPH-SVRCDC01$
192.168.210.17  ZPH-SVRCHR$
192.168.210.18  ZPH-SVRCSUP$
192.168.210.19  ZSM-SVRCSQL02$
192.168.210.101 INT-MAINT$
```

### Gaining Access


### Maintaining Access


# Random Notes