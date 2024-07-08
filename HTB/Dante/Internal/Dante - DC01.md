# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: 172.16.1.20

# Findings
### Credentials
`FoundCREDs`

### Flag
1. `DANTE{Feel1ng_Blu3_or_Zer0_f33lings?}`
2. `DANTE{1_jusT_c@nt_st0p_d0ing_th1s}`
## External
### Enumeration
- I did a Responder and there was a request Back from `172.16.1.20` so i started with it
![](https://i.imgur.com/IdhpiKL.png)
` 172.16.1.12 `
` 172.16.1.19 `

![](https://i.imgur.com/VwKFhZc.png)
- We have some ADCS
	- https://dante-dc01/CertEnroll/DANTE-DEV-CA.crl
`datne`
### Gaining Access
- I Havent Got Nothing, so i went to check Exploits, it is `windows 2012` so there will some bugs
![](https://i.imgur.com/0pj6MEz.png)
- It was not working so i changed the exploit to eternal romance
![](https://i.imgur.com/xsX40QF.png)
![](https://i.imgur.com/dO88eBK.png)
## Internal
### Enumeration
![](https://i.imgur.com/sv0LmuC.png)
![](https://i.imgur.com/JyuAQU6.png)
`Administrator:500:aad3b435b51404eeaad3b435b51404ee:9bff06fe611486579fb74037890fda96`
![](https://i.imgur.com/axlguHe.png)
- It worked with the defaul password i got from the secretdump.
` katwamba : DishonestSupermanDiablo5679 `
![](https://i.imgur.com/slGzoSB.png)
![](https://i.imgur.com/RLgRodt.png)
![](https://i.imgur.com/8DqcMjp.png)
`impacket-psexec katwamba:DishonestSupermanDiablo5679@172.16.1.20`
### Gaining Access
- Browser Files, `place.sqlite` you can get browser history...
![](https://i.imgur.com/RsqZBF6.png)

![](https://i.imgur.com/Kva4Ylu.png)
- I did Double pivot with ligolo
![](https://i.imgur.com/3RerhNb.png)
[[Dante - DC02]]


```
client -v 172.16.1.100:1234 socks
```
### Maintaining Access


# Random Notes