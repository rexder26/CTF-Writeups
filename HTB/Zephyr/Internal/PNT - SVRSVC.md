# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `192.168.110.52`

# Findings
### Credentials
`painters.htb\web_svc:!QAZ1qaz`

### Flags
- `ZEPHYR{S3rV1c3_AcC0Un7_5PN_Tr0uBl35}`
## External
### Enumeration
```
PORT     STATE SERVICE       REASON         VERSION
135/tcp  open  msrpc         syn-ack ttl 64 Microsoft Windows RPC
139/tcp  open  netbios-ssn   syn-ack ttl 64 Microsoft Windows netbios-ssn
445/tcp  open  microsoft-ds? syn-ack ttl 64
3389/tcp open  ms-wbt-server syn-ack ttl 64 Microsoft Terminal Services
| rdp-ntlm-info:
|   Target_Name: PAINTERS
|   NetBIOS_Domain_Name: PAINTERS
|   NetBIOS_Computer_Name: PNT-SVRSVC
|   DNS_Domain_Name: painters.htb
|   DNS_Computer_Name: PNT-SVRSVC.painters.htb
|   DNS_Tree_Name: painters.htb
|   Product_Version: 10.0.20348
|_  System_Time: 2024-06-27T08:27:34+00:00
| ssl-cert: Subject: commonName=PNT-SVRSVC.painters.htb
| Issuer: commonName=PNT-SVRSVC.painters.htb
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2024-06-25T16:06:00
| Not valid after:  2024-12-25T16:06:00
| MD5:   f569:8ab6:5299:51e9:b65d:d557:4709:dbc1
| SHA-1: fe25:6645:06bc:e04e:6cc2:5a58:0f67:b1ab:e686:c5bb
| -----BEGIN CERTIFICATE-----
| MIIC8jCCAdqgAwIBAgIQGDwGHXJVRrxOjALj6Zo0oDANBgkqhkiG9w0BAQsFADAi
| MSAwHgYDVQQDExdQTlQtU1ZSU1ZDLnBhaW50ZXJzLmh0YjAeFw0yNDA2MjUxNjA2
| MDBaFw0yNDEyMjUxNjA2MDBaMCIxIDAeBgNVBAMTF1BOVC1TVlJTVkMucGFpbnRl
| cnMuaHRiMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3uXCGkefEANZ
| OiKo/tXiEjWU0+t0h0o+TJ/0Y6h8JgGtG/itMKFEkk09CW244rOx5zjkzxeXhij+
| bbWE6CsWFctzr79aCbgZz5/qr9CHvNMtVT2xKTyyTl0pgBskGgulhntYsHcPw7Nk
| EDDjNlQXpbigcEdLq9/zvrWKMTucyNVfKXa+bwdAso6WX0Z0bFNXco+OZdvKOP6W
| RFzV1uIPO8npclpxWnfQdBa1nnEztCsofw5YfwMG1VK+VgYcwqWE2I7fFDVwpHHU
| hEh/Z59xGGt/s1RoIKnW+W2CLELHl6sd7KSMrzuobIKXN5kQYEDpNF+6yZKUEJf/
| SJyjWIR9SQIDAQABoyQwIjATBgNVHSUEDDAKBggrBgEFBQcDATALBgNVHQ8EBAMC
| BDAwDQYJKoZIhvcNAQELBQADggEBAE4180+bi1wgFWLVFBrfpgJK1V7AOf9qGarF
| 5HXFIUiQ6odZ3hOpil/UUMZc0kJBc/4VNzs+1hzHtmnCeeDv6/CeRWlzkFhGNbl4
| c+85blTsyh9tpuvjNpe0z/4nb4gAMCQgJvbvO3EmzUCNuYNz+ImCi1rfkiifWQJm
| NGJ1QMgv+1U4d8dJml60P2jlekXUnLymjuyVhoXNnto64pzImmKAg8sps1E4c8Ih
| tn2u2v/I9E1ELrjqYwtqNt6NNK7S1X1tIwt6cvDi2f5D2JU+ttXITqL9mD0Vv51T
| SVaQzrkjFL9uxr2vy8R7MpMY0mhQFdbfQW/W8ovqopCpeNsoZP0=
|_-----END CERTIFICATE-----
|_ssl-date: 2024-06-27T08:27:44+00:00; +6s from scanner time.
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows
```
![](https://i.imgur.com/C6hLbvd.png)
`painters.htb\web_svc:!QAZ1qaz (Pwn3d!)`
### Gaining Access
![](https://i.imgur.com/THBNFcY.png)
![](https://i.imgur.com/eLto3bz.png)
- if i have all the privs that means am an admin
![](https://i.imgur.com/SndVOq5.png)
## Internal
### Enumeration
![](https://i.imgur.com/CumcNBI.png)
```shell
[*] Dumping cached domain logon information (domain/username:hash)
PAINTERS.HTB/Administrator:$DCC2$10240#Administrator#4f3d8c09f46360e84463d125c240c554: (2023-12-15 06:13:08)

[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:6ee87fa6593a4798fe651f5f5a4e663e:::
James:1001:aad3b435b51404eeaad3b435b51404ee:8af1903d3c80d3552a84b6ba296db2ea:::
```
[[PNT - SVRBPA]]
![](https://i.imgur.com/j8E2K02.png)
`WINRM       192.168.110.56  5985   NONE             [+] None\riley:P@ssw0rd (Pwn3d!)`
- i got stuck and i temembered the hashes i got, 1 thing i forgot was i didnt tried them on local computer with `-d .`
![](https://i.imgur.com/nP2cpIr.png)
[[PNT - SVRBPA]]
### Gaining Access


### Maintaining Access


# Random Notes