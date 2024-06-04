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
![](https://i.imgur.com/xFjW9Ij.png)
#### Port `80`
- `C:\webroot`
![](https://i.imgur.com/kXSxrG5.png)
![](https://i.imgur.com/ZkTOSid.png)
- It looks Something
```
Ask-Jeeves-whatever-happened-to-32225327-270-301
joival
```
![](https://i.imgur.com/Ub9NjH7.png)
https://what.thedailywtf.com/topic/10487/fractal-reporting/19?_=1715450326969&lang=en-US
- I got nothing, so i started looking and there is `?` so i tried to fuzz for parameters too
![](https://i.imgur.com/ehP1Fwe.png)

#### Port `445`
![](https://i.imgur.com/ZMick0s.png)

- After so much hour of enum, i havent got any thing good, so i check writeup and i got `askjeeves` endpoint on the port `50000` but that was not in any of ma computer wordlists.
### Gaining Access
![](https://i.imgur.com/A470QMj.png)
![](https://i.imgur.com/A2UFiWG.png)
![](https://i.imgur.com/i5gdzvG.png)

## Internal
### Enumeration
![](https://i.imgur.com/fb0MV8B.png)

![](https://i.imgur.com/NreurSC.png)

![](https://i.imgur.com/fQJaJh6.png)
C:\Users\kohsuke\AppData\Local\Temp
JENKINS_HOME: C:\Users\Administrator\.jenkins
### Gaining Access


### Maintaining Access
![Uploading file...fgry1]()
```shell
 C:\Program Files\CMAK
    C:\Program Files\Common Files
    C:\Program Files\desktop.ini
    C:\Program Files\Internet Explorer
    C:\Program Files\rempl
    C:\Program Files\Uninstall Information
    C:\Program Files\UNP
```
![](https://i.imgur.com/y733gnv.png)
![](https://i.imgur.com/MJoUtvr.png)
` moonshine1  :     (jeeves) `
![](https://i.imgur.com/N1C5Jho.png)
![](https://i.imgur.com/BCae7N6.png)

# Random Notes
hudson.util.Secret.decrypt(cmc1l9rhCIG9l/GpTwgOTy5u5Ee4BUzNQRs67vZI8/ZHD37MnEgrORjgOIyi5E6KaLhjGR/iCbyN506ih50AtZUQeRAtLOt0Fbezl+USLHqsgA2TZjwi2QAFB+kbVgeXI9wb+ZKhTUkn3S3oWxkIyA==)