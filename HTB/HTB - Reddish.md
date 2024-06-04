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
![](https://i.imgur.com/it2003x.png)
![](https://i.imgur.com/Z7vcsDe.png)
- When i change the request method this happened.
	- ![](https://i.imgur.com/paSnjhq.png)
```json
{"id":"fe3b8cb2a67e3a14547f5f797a7d0f3e","ip":"::ffff:10.10.14.36","path":"/red/{id}"}
```
https://quentinkaiser.be/pentesting/2018/09/07/node-red-rce/
- `"_credentialSecret": "3edbd7dcb66be920fcae7b7f0b988a23efb99c61b3891cd932ef17cbff777adf"`
```shell

/home/aryeh/test555555

$2a$08$zZWtXTja0fB1pzD4sHCMyOCMYz2Z6dNbM6tl8sJogENOMcxWV9DN.
test/red/api/auth/users_spec.js:30:                    password:'$2a$08$LpYMefvGZ3MjAfZGzcoyR.1BcfHh4wy4NpbN.cEny5aHnWOqjKOXK',

this machine
172.18.0.2	nodered
172.19.0.4	nodered

```
![](https://i.imgur.com/nQQnO0r.png)

### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes