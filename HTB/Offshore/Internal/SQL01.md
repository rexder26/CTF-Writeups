# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `.15`

# Findings
### Credentials
`FoundCREDs`

### Flags
- `OFFSHORE{hmm_p0tato3s}`
- `OFFSHORE{cm0n!_an0th3r_sqli!?}`
## External
### Enumeration
```
PORT     STATE SERVICE       REASON         VERSION
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds  syn-ack ttl 64 Microsoft Windows Server 2008 R2 - 2012 microsoft-ds
1433/tcp open  ms-sql-s      syn-ack ttl 64 Microsoft SQL Server 2014 12.00.2000.00; RTM
| ms-sql-ntlm-info:
|   172.16.1.15:1433:
|     Target_Name: CORP
|     NetBIOS_Domain_Name: CORP
|     NetBIOS_Computer_Name: SQL01
|     DNS_Domain_Name: corp.local
|     DNS_Computer_Name: SQL01.corp.local
|     DNS_Tree_Name: corp.local
|_    Product_Version: 10.0.14393
| ms-sql-info:
|   172.16.1.15:1433:
|     Version:
|       name: Microsoft SQL Server 2014 RTM
|       number: 12.00.2000.00
|       Product: Microsoft SQL Server 2014
|       Service pack level: RTM
|       Post-SP patches applied: false
|_    TCP port: 1433
|_ssl-date: 2024-07-02T08:36:57+00:00; +39s from scanner time.
| ssl-cert: Subject: commonName=SSL_Self_Signed_Fallback
| Issuer: commonName=SSL_Self_Signed_Fallback
| Public Key type: rsa
| Public Key bits: 1024
| Signature Algorithm: sha1WithRSAEncryption
| Not valid before: 2024-07-02T03:20:13
| Not valid after:  2054-07-02T03:20:13
| MD5:   6e56:768a:268a:c5ae:f4a9:aac2:bf25:8268
| SHA-1: 35d1:8565:082d:2d1f:1ddb:919e:c3e9:ad61:0e94:ee04
| -----BEGIN CERTIFICATE-----
| MIIB+zCCAWSgAwIBAgIQecxlS8Wm2K9F/EmpIWFmeTANBgkqhkiG9w0BAQUFADA7
| MTkwNwYDVQQDHjAAUwBTAEwAXwBTAGUAbABmAF8AUwBpAGcAbgBlAGQAXwBGAGEA
| bABsAGIAYQBjAGswIBcNMjQwNzAyMDMyMDEzWhgPMjA1NDA3MDIwMzIwMTNaMDsx
| OTA3BgNVBAMeMABTAFMATABfAFMAZQBsAGYAXwBTAGkAZwBuAGUAZABfAEYAYQBs
| AGwAYgBhAGMAazCBnzANBgkqhkiG9w0BAQEFAAOBjQAwgYkCgYEAn5ymY1W7YJsj
| 2/nnjnuvypuuHRXrrfRmkpnl+7ama4fMGJ0kXS8yNGdc3o6+9Rw17mPRcTFgRqQu
| Ukf37tq2MdgduNWCQwIv+XeCCe0FCXlhXt6mrb1YpMvbWU4fX+1Y8L9JaNwZfmsl
| I0gLIHeAWplsb9kZTuhl8NVc5p7X2ykCAwEAATANBgkqhkiG9w0BAQUFAAOBgQBZ
| hEFiH4DlYKDlmD4ejPZMYz9rjct4amRFcBPhdkpv52SRS9TZMvo3wUBzHBtPLR/d
| n074CWl3zvYvS5thFJtolSZMJTVKbwN3TWPsmVth52bZY7cygWyy4cVqK5EKQO6M
| aYUhW/sZ9rmt3fDDWHvlvg4077+eEcehztDPr2oSrA==
|_-----END CERTIFICATE-----
3389/tcp open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: CORP
|   NetBIOS_Domain_Name: CORP
|   NetBIOS_Computer_Name: SQL01
|   DNS_Domain_Name: corp.local
|   DNS_Computer_Name: SQL01.corp.local
|   Product_Version: 10.0.14393
|_  System_Time: 2024-07-02T08:36:46+00:00
```
### Gaining Access
[[WEB-WIN01]]
![](https://i.imgur.com/00lv6Ag.png)
![](https://i.imgur.com/hM6Ux4s.png)
![](https://i.imgur.com/V4hEthl.png)
`administrator: 7facdc498ed1680c4fd1448319a8c04f`
![](https://i.imgur.com/DjtRlpo.png)
`Carrot dog fish cat tree frog1!`

C:\Users\iamtheadministrator\Documents\SQL Server Management Studio\Settings\SQL Server Management Studio\NewSettings.vssettings
 C:\Users\Administrator\Documents\SQL Server Management Studio\NewSettings.vssettings
## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes