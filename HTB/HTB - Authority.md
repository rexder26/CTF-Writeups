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
## External
### Enumeration
![](https://i.imgur.com/NKig25D.png)
![](https://i.imgur.com/OTS02rR.png)
![](https://i.imgur.com/VOBQQNx.png)
![](https://i.imgur.com/nMJcyVu.jpeg)
f
![](https://i.imgur.com/uBG1MiH.png)
-> ADCS
![](https://i.imgur.com/IJo4AAv.png)
```shell
ca_own_root: yes

# A passphrase for the CA key.
ca_passphrase: SuP3rS3creT

# The common name for the CA.
ca_common_name: authority.htb

# Other details for the CA.
ca_country_name: NL
ca_email_address: admin@authority.htb
ca_organization_name: htb
ca_organizational_unit_name: htb
ca_state_or_province_name: Utrecht
ca_locality_name: Utrecht


pwm_hostname: authority.htb.corp
pwm_http_port: "{{ http_port }}"
pwm_https_port: "{{ https_port }}"
pwm_https_enable: true

pwm_require_ssl: false

pwm_admin_login: !vault |
          $ANSIBLE_VAULT;1.1;AES256 326665343864353665376531366637316331386162643232303835663339663466623131613262396134353663663462373265633832356663356239383039640a346431373431666433343434366139356536343763336662346134663965343430306561653964643235643733346162626134393430336334326263326364380a6530343137333266393234336261303438346635383264396362323065313438

pwm_admin_password: !vault |
          $ANSIBLE_VAULT;1.1;AES256 313563383439633230633734353632613235633932356333653561346162616664333932633737363335616263326464633832376261306131303337653964350a363663623132353136346631396662386564323238303933393362313736373035356136366465616536373866346138623166383535303930356637306461350a3164666630373030376537613235653433386539346465336633653630356531

ldap_uri: ldap://127.0.0.1/
ldap_base_dn: "DC=authority,DC=htb"
ldap_admin_password: !vault |
          $ANSIBLE_VAULT;1.1;AES256 633038313035343032663564623737313935613133633130383761663365366662326264616536303437333035366235613437373733316635313530326639330a643034623530623439616136363563346462373361643564383830346234623235313163336231353831346562636632666539383333343238343230333633350a6466643965656330373334316261633065313363363266653164306135663764

ansible_user: administrator
ansible_password: Welcome1
ansible_port: 5985
ansible_connection: winrm
ansible_winrm_transport: ntlm
ansible_winrm_server_cert_validation: ignore

remote user = svc_pwm
```
https://www.bengrewell.com/cracking-ansible-vault-secrets-with-hashcat/
![](https://i.imgur.com/DgIx3Jp.png)
- ` ansible : !@#$%^&* `
![](https://i.imgur.com/FmbkpOg.png)
- `pWm_@dm!N_!23` - the password worked on the configuration manager port `8443`
![](https://i.imgur.com/FHCI9JW.png)
```xml
<property key="configPasswordHash">$2a$10$gC/eoR5DVUShlZV4huYlg.L2NtHHmwHIxF3Nfid7FfQLoh17Nbnua</property>

<setting key="pwm.securityKey" modifyTime="2022-08-11T01:46:23Z" syntax="PASSWORD" syntaxVersion="0">
            <label>Settings ⇨ Security ⇨ Application Security ⇨ Security Key</label>
            <value>ENC-PW:O9oCDo+C6OFRcAvdOIS1giHOhecQQnPxYlI4SA5gJ/39uow2EnmDNTokudsIgPivKue/Um6dkZm1RrcECBHk358zc045rDyFL2fDku2kusl79NE+Tww8gC8QQ0CX+VS2yyD46+ZS6Jriyu1Y7BOXnJifXXXsHzTmBTkodvnY33V6Puc0Zze0PGYHN+CGFtx/g5WaBTQbQwZwNLA+8Qe11GqCz+rBjGzQp0w6yLHJn+ZYBlLWgvZwN2KUHOiUIq5eKKDgjv+mga4zcB1STcpMJRaIiSnLdY3VCfsEj6p4BGz9jj+N7gQHBFAvI05JexXq8HyL7ZUEzLXU5FMQXvhhWSbhxoz7LH/iamvoOg13WnI3MRUzrXv91Uh7gdNZuXa1NmSBOe/g1GgmFV+0sxLIJ/99VT+GHIwrfjPNNV6jtKHhURPwp0a38c6aBGjpvB3AgAoZ0/KVLvQK1pAevO4NK2XFF2nPD8gQCQJMCsb62I+XMitkO2zKytrYEwZhl9VUGF0bAXQhC5I9xX1tEQAGBcENt1NGfM8iE+PlrZWwlr1yDjw+GZEm2KHyjnUFpBubqD7l7mvEJbEV26SQkR0v4R5LSEPbElOKGbGXMKkDEi53SQ5P0ZZQbega9XtBOHs+/s1EZ4p/qGVCvpD9dgc0SyS0auXU0PUddjxyXthHdqRbEWHhAduXYQgXF0eM2yWlbd7fTgSUMERlpjdFX/QZG3D6Ghp+iOCwfelEfKMQDO1myQcpq5YTE94YDz+aSWvi7ZGRIq+hRkwuR8E0EbEUE7CApDwF3LjGi+UEd9Y3Q9SPSMVxg4Ra2FB4sYCT19N7KV3TpGvJYD4SE8Mrn0cH9ihvlvDJFOxoLC9xM8FA9EAvSZN1w6lV4pUsVpUSM0LRKLqCmBCRJvaRNbhRymM96NFSSi4PwCCJQ7WVJjiS+oLQ+7qwHhqLQFy0+gtkGSQnBoq1FMYSCyGz/fUG84Xe0CSTPt4SwTq+L2M2jqsiB+HXq1z2LdkAFo6xm1Mqs6H/x5ZP1esjvRxDzHod31jRizu+rJw4LNRb172A36dQWmiq/OJQBJrnPu87s+KmoNyCJGrT2+1QttMgM62qy2/Eb6xByQ8RiLl6v87vf24TuWhxJhXfNWMRuHXJp2IWt5BWAYdiQNUjCuvRhfiyxsIqelpEpsOnm8WDVEsN0hqaEt9Db2e/d3Wpx1as4luVtA/MZtKy+gsH0qZUmouj7LCfN5TJpm00MiBTxYSkapKvAGchkE4UVc3AHGIxeyy+t2LwqT9fDSlS/VofOELNcQD3OfPi+asOrgaqcRbZVXdQumoJsubLMiPpHTZtOH2Nt13cEh9ZG/XebrAkchsMjsyLo5KX0nL6RKbMNUA3BmM2cd+bjj+Jar2aeAeqBdW+LU5ALshAsF986N1BGSsQ8aZkJwLi3PUYG8vGR88ZqEMMziQ=</value>
        </setting>

<setting key="ldap.proxy.password" modifyTime="2022-08-11T01:46:23Z" profile="default" syntax="PASSWORD" syntaxVersion="0">
            <label>LDAP ⇨ LDAP Directories ⇨ default ⇨ Connection ⇨ LDAP Proxy Password</label>
            <value>ENC-PW:We9gQUqI/5SppKB6XccIzT/MGhRE8E+ak4pEGIknoluQOv8vpUvwMPccEt+KRwMxTYfsZfkLaNHbjGfbQldz5EW7BqPxGqzMz+bEfyPIvA8=</value>
        </setting>
```
### Gaining Access
![](https://i.imgur.com/2awLT8v.jpeg)
![](https://i.imgur.com/LlmhYyU.png)
```shell
svc_ldap : lDaP_1n_th3_cle4r!
```
![](https://i.imgur.com/1PrcF5z.png)

## Internal
### Enumeration
- i have seen ADCS on the Share so i tried to do ADCS abuse
![](https://i.imgur.com/os49yYT.jpeg)
- and i saw there is `ESC1` so i exploited that

### Gaining Access


### Maintaining Access


# Random Notes