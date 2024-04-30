# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #dnsadmin #powershellhistory #ldap

# Findings

## External
### Enumeration
![](https://i.imgur.com/YVgFmye.png)
![](https://i.imgur.com/3yPt3WN.png)

`megabank.local`
![](https://i.imgur.com/k3QQwdo.png)
![](https://i.imgur.com/HcEtHIz.png)
- the account lock threshld is 0 means, i can Bruteforce it.
	- No luck
- ![](https://i.imgur.com/1Bjwg6j.png)
![](https://i.imgur.com/RSBweqk.png)
![](https://i.imgur.com/kwIX7mU.png)
` melanie : Welcome123! `
### Gaining Access
- It Doesnt work for the marko, so i did password spray![](https://i.imgur.com/mXmcx02.png)
- ![](https://i.imgur.com/qiAMwDo.png)
## Internal
### Enumeration
![](https://i.imgur.com/8E3hPiL.png)

![](https://i.imgur.com/aIZGjz1.png)

```
lsadump::dcsync /domain:testlab.local /user:Administrator
```
![](https://i.imgur.com/vvpGkXK.png)
![](https://i.imgur.com/h0ukNQw.png)
- `ryan : Serv3r4Admin4cc123!`
- ![](https://i.imgur.com/EHjg4ZC.png)
- ![](https://i.imgur.com/TYjRvkS.png)
- This Means I can do the DNS admin attack.
### Gaining Access
![](https://i.imgur.com/px4Y3VI.png)
![](https://i.imgur.com/UoSde1F.png)
![](https://i.imgur.com/2AGfsrF.png)
### Maintaining Access


# Random Notes