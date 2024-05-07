# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #ApacheOFbiz 

Hello Guys, Today i was little bit Distracted but i was trying to plan the `Bizness` CTF from HTB, it looks Easy But it took me a lot also done with some little help. Enjoy ...
# Findings

## External
### Enumeration
- I started My Simple nmap to make things quick.
	- ![](https://i.imgur.com/BfkLvbT.png)
- While the nmap scan i was checking the site, also running my Directory Bruteforce with fuff
	- It was little bit hard to pass the self-signed cert on ffuf, Because i havent tried that before.
	- ![](https://i.imgur.com/jADjDAY.png)
- The site footer Contains a Powered by text
	- ![](https://i.imgur.com/hylZsnv.png)
- Also my ffuf have got 1 directory saying control so I tried to access the page. but it throw an error, but we can grab some information from the error, i confirmed that the site have some thing called `Apache OFbiz`.
	- ![](https://i.imgur.com/sj9tFjE.png)
### Gaining Access
- I tried to Google if there is any exploit for this and i got 1 that can do [authentication bypass](https://github.com/jakabakos/Apache-OFBiz-Authentication-Bypass)
![](https://i.imgur.com/10yZWmh.png)
- Then I started my listener
![](https://i.imgur.com/qZwHZDR.png)
- and executed the exploit
![](https://i.imgur.com/KsrFNBT.png)
- Boom We got Shell.
![](https://i.imgur.com/JSobsG0.png)
- We got user flag.
![](https://i.imgur.com/kxVRy9S.png)
## Internal
### Enumeration
- Tried to Enumerate many directories for password and some sensitive data manually but things we got are not working.
![](https://i.imgur.com/ZLSv4Lg.png)
- Tried To access the file `docker/docker-entrypoint.sh` most of the time there might be some configurations over there(from experience)
- I found this on the page
![](https://i.imgur.com/CbT2C8l.png)
- it shows that they are useing `SHA1`with  salt and also there is a path for the file opening `framework/resources/templates/AdminUserLoginData.xml`.
![](https://i.imgur.com/H7Jb1Ff.png)
- as you see there is a currentPassword hash, it says some SHA, so the hash is sha with some prefix salt.
- It was not HelpFull so i stack over here, at this point i tried to get some help, and found out to check the databse thing, that the apache ofbiz uses a database called Derby.
![](https://i.imgur.com/sc9t6P2.png)
- and this database files have extention of `.dat`. So i tried to list all the `.dat` files on the computer.
![](https://i.imgur.com/iRD03Zi.png)
- As you see almost all are from this path `/runtime/data/derby/ofbiz/seg0` so went there and tried to Find anything containing `SHA` with ma beloved `strings` and `grep` tool.
![](https://i.imgur.com/7EtWL3D.png)
- as you see we got `$SHA` Hash. So lets Crack this Hash, when i try john it says no password hash. 
![](https://i.imgur.com/YwgY7E3.png)
- Lets google how to crack derby sha 
![](https://i.imgur.com/7UdklhP.png)
- Used this tool and cracked the Hash.
![](https://i.imgur.com/BE66qVU.png)
### Maintaining Access
- we tried to use it to be root with `su` and it worked!! and Got root flag.
![](https://i.imgur.com/QmlELO4.png)
THANK YOUUUU

# Random Notes
config
applications
/ofbiz/docker-entrypoint.sh"
/ofbiz/config


	- So i Tried Chat GPT to tell me where i get any sensetive data or configirations about the apache ofbiz .
		- ![](https://i.imgur.com/8PK3y3h.png)

`<UserLogin userLoginId="@userLoginId@" currentPassword="{SHA}47ca69ebb4bdc9ae0adec130880165d2cc05db1a" requirePasswordChange="Y"/>`

```java
# Create and load the password hash for the admin user.                                                     
load_admin_user() {                                     
  if [ ! -f "$CONTAINER_ADMIN_LOADED" ]; then                                
    TMPFILE=$(mktemp)      
                                         
    # Concatenate a random salt and the admin password.                                 
    SALT=$(tr --delete --complement A-Za-z0-9 </dev/urandom | head --bytes=16)     
    SALT_AND_PASSWORD="${SALT}${OFBIZ_ADMIN_PASSWORD}"                                                                                     
    # Take a SHA-1 hash of the combined salt and password and strip off any additional output form the sha1sum utility.                           
    SHA1SUM_ASCII_HEX=$(printf "$SALT_AND_PASSWORD" | sha1sum | cut --delimiter=' ' --fields=1 --zero-terminated | tr --delete '\000') 


    # Convert the ASCII Hex representation of the hash to raw bytes by inserting escape sequences and running                                                                                                                                 
    # through the printf command. Encode the result as URL base 64 and remove padding.                                                                                                                                                        
    SHA1SUM_ESCAPED_STRING=$(printf "$SHA1SUM_ASCII_HEX" | sed -e 's/\(..\)\.\?/\\x\1/g')                                                                                                                                                     
    SHA1SUM_BASE64=$(printf "$SHA1SUM_ESCAPED_STRING" | basenc --base64url --wrap=0 | tr --delete '=')                                                                                                                                        
                                                                                                                                                                                                                                              
    # Concatenate the hash type, salt and hash as the encoded password value.                                                                                                                                                                 
    ENCODED_PASSWORD_HASH="\$SHA\$${SALT}\$${SHA1SUM_BASE64}"                                                                                                                                                                                 
                                                                                                                                                                                                                                              
    # Populate the login data template                                                                                                                                                                                                        
    sed "s/@userLoginId@/$OFBIZ_ADMIN_USER/g; s/currentPassword=\".*\"/currentPassword=\"$ENCODED_PASSWORD_HASH\"/g;" framework/resources/templates/AdminUserLoginData.xml >"$TMPFILE"                                                        
                                                                                                                                                                                                                                              
    # Load data from the populated template.                                                                                                                                                                                                  
    /ofbiz/bin/ofbiz --load-data "file=$TMPFILE"                                                                                                                                                                                              
                                                                                                                                                                                                                                              
    rm "$TMPFILE"                                                                                                                                                                                                                             
                                                                                                                                                                                                                                              
    touch "$CONTAINER_ADMIN_LOADED"                                                                                                                                                                                                           
  fi                                                                                                                                                                                                                                          
}
```

/opt/ofbiz/applications/order/minilang/customer/CustomerEvents.xml
/opt/ofbiz/framework/security/ofbiz-component.xml

![](https://i.imgur.com/lnGDkQq.png)


/opt/ofbiz/runtime/data/derby/ofbiz/seg0
https://github.com/duck-sec/Apache-OFBiz-SHA1-Cracker
