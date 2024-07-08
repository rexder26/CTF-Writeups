# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
`FoundCREDs`

### Flag
- `DANTE{H1ding_1n_th3_c0rner}`
- `DANTE{Alw4ys_check_th053_group5}`
## External
### Enumeration
![](https://i.imgur.com/MVAIxEr.png)
- tried to login with julian and it worked

### Gaining Access

![](https://i.imgur.com/OEGfCIY.png)
` julian : manchesterunited `
## Internal
### Enumeration
![](https://i.imgur.com/wcitLbZ.png)
- ` sophie : TerrorInflictPurpleDirt996655` -> it is for [[Dante - SQL01]]
### Gaining Access
```
/home/plongbottom/.bash_history

2020-07-01+23:03:11.9794801860 /etc/console-setup/cached_setup_terminal.sh
2020-07-01+23:03:11.9794801860 /etc/console-setup/cached_setup_font.sh
2020-07-01+23:03:11.9714801850 /etc/console-setup/cached_setup_keyboard.sh

   101168      4 -rw-r--r--   1 julian   julian        211 Jul 15  2020 /var/mail/note
   101168      4 -rw-r--r--   1 julian   julian        211 Jul 15  2020 /var/spool/mail/note

-rw-r--r-- 1 root root 2906 Jun 30  2020 /etc/apt/sources.bak
```
![](https://i.imgur.com/fqgF5me.png)
- i tool the username of the another user from the machine and tried to bruteforce it
![](https://i.imgur.com/sFXJ9Jr.png)
`plongbottom : PowerfixSaturdayClub777`
### Maintaining Access
![](https://i.imgur.com/7Ej9qGJ.png)


# Random Notes