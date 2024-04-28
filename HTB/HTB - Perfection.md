# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings

## External
### Enumeration
`$enum$`

### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes
![](https://i.imgur.com/RofA60y.png)
![](https://i.imgur.com/hma0wUC.png)
![](https://i.imgur.com/QEwos2l.png)
![](https://i.imgur.com/9FHnno7.png)
![](https://i.imgur.com/SGZrk51.png)
- I can use 1 row only
- ![](https://i.imgur.com/K1Znb2s.png)- 

- ![](https://i.imgur.com/ED9t7di.png)
Thinking to Fuzz it but, the website is just calculating some result so it cant be SQLi,XSS or XXE maybe from the wordliss..... tempalte enginer can be good
![](https://i.imgur.com/6RiFLEv.png)
we are good
![](https://i.imgur.com/i0KSxkB.png)
There is something over here
![](https://i.imgur.com/urAJgSt.png)
- i thought to encode it ![](https://i.imgur.com/ZO0oBRs.png)
![](https://i.imgur.com/l8bntzS.png)
- Ohhh cool cool cool , they are using ruby template engine![](https://i.imgur.com/DnOSoGE.png)
- as we know they are using ruby server... sooo i think we are on good now
- i got that they are blocking any `%` signs.
	- ![](https://i.imgur.com/XEb7TLl.png)
i was Researching how i can bypass this and i got this [blog](https://blog.devops.dev/ssti-bypass-filter-0-9a-z-i-08a5b3b98def)
![](https://i.imgur.com/fkiiwSq.png)

![](https://i.imgur.com/nygRcjo.png)
- Boom BOOM BOOM
	- ![](https://i.imgur.com/KyPQsM8.png)
	![](https://i.imgur.com/C9OH2pO.png)
![](https://i.imgur.com/M7VHyOt.png)
- we got the shell
- ![](https://i.imgur.com/MRlokdb.png)
- we got the root flag
	- ![](https://i.imgur.com/kosB0kI.png)
# Priviliege escalation
![](https://i.imgur.com/IvWTWVp.png)
- [x] check `id`
- [ ] and that database file
	- [ ] know the encryption
- [x] check he crontab
- [ ] /home/susan/.sqlite_history
- [ ] /home/susan/.bash_history
- [ ] /usr/bin/crontab
- [ ] ./etc/ldap
![](https://i.imgur.com/0uNTYJr.png)
[Configuration]
AdminIdentities=unix-user:0
[Configuration]
AdminIdentities=unix-group:sudo;unix-group:admin


after 1 hour stuck, i got brain damange and asked for help, then someone told me to check for mails.
 then forund this
	 ![](https://i.imgur.com/VAbdUvu.png)
- This i asked GPT for python script
	- ![](https://i.imgur.com/94OWE9a.png)

- Password Crack
	- d
- ![](https://i.imgur.com/gacqXA8.png)
![](https://i.imgur.com/twuq8OM.png)
