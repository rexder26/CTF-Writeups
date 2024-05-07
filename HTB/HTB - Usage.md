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

![](https://i.imgur.com/K2IgZne.png)

![](https://i.imgur.com/MXxbLKH.png)
![](https://i.imgur.com/eNEAmOz.png)
![](https://i.imgur.com/JdNf5A4.png)


```
admin.usage.htb/admin/auth/login
admin.usage.htb/vendor/laravel-admin/AdminLTE/plugins/iCheck/square/blue.css

```

![](https://i.imgur.com/YpMSPqt.png)

```shell
echo "eyJpdiI6ImJtOUtBS0wyL2oyTWFUSkNrRU9uNnc9PSIsInZhbHVlIjoic1F6YmxOMlRUZG1NbzNCM
m1VeW1Mbi9yeDk4VDd5UnNSS2NZVkpKa09XQTVnbEpXRVVYcVZFVTZqdkdFY3NRSmdKZUpxNmE0YkdkSjMraFUyOU00SmZORDNhWk91ZFkyVGFyVk4zdFFpV05kQ1ZVMEZqUlRlbERJNk5oNTdwejIiLCJtYWMiOiIzYjEwNmU4NWUxZGY0MTNhZTFhOTg1ZWNiZDE1ZmU3YmU1OGRkN2UxZGY1YTk1NWM2OWQxNWIxODliYjRhZDI2IiwidGFnIjoiIn0=" | base64 -d                                           
```
```json
{
"iv":"bm9KAKL2/j2MaTJCkEOn6w==",
"value":"sQzblN2TTdmMo3B2mUymLn/rx98T7yRsRKcYVJJkOWA5glJWEUXqVEU6jvGEcsQJgJeJq6a4bGdJ3+hU29M4JfND3aZOudY2TarVN3tQiWNdCVU0FjRTelDI6Nh57pz2",
"mac":"3b106e85e1df413ae1a985ecbd15fe7be58dd7e1df5a955c69d15b189bb4ad26",
"tag":""
}
```
**Laravel Deserialization RCE**

### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes