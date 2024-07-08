# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `192.168.110.56`

# Findings
### Credentials
`FoundCREDs`
## External
### Enumeration
![](https://i.imgur.com/tRSOkdN.png)
- ` riley :P@ssw0rd`
![](https://i.imgur.com/OaiLpjO.png)
![](https://i.imgur.com/9DQWJQ7.png)
```python
import requests
import subprocess
import time
import os
import warnings

warnings.filterwarnings("ignore")

url = "https://painters.htb/administration"
username = "admin"
password = "Mail4Painter2022!@#"

with requests.Session() as s:
    s.post(f"{url}/login", data={"username": username, "pass": password}, verify=False)

    for i in range(1,10):
        pdf_opened = False
        try:
            print(f"Opening PDF {i}")
            response = s.post(f"{url}/application/download", data={"application_id": i}, verify=False)
            response.raise_for_status()

            pdf_content = response.content
            if len(pdf_content) == 0:
                continue

            with open(f"{os.getcwd()}\pdf{i}.pdf", "wb") as f:
                f.write(pdf_content)

            subprocess.Popen([f"C:\Program Files (x86)\Adobe\Acrobat Reader DC\Reader\AcroRd32.exe", f"{os.getcwd()}\pdf{i}.pdf"])

            time.sleep(3)

            pdf_opened = True

        except Exception as e:
            print(f"Error: {e}")
        finally:
            if pdf_opened:
                subprocess.Popen(["TASKKILL", "/F", "/IM", "AcroRd32.exe", "/T"])
                time.sleep(2)

        if os.path.exists(f"{os.getcwd()}\pdf{i}.pdf"):
            os.remove(f"{os.getcwd()}\pdf{i}.pdf")

    response = s.get(f"{url}/application/purge", verify=False)
    if "Successfully purged database entries." in response.text:
        print("Script execution successful")
    else:
        print("Failed to purge database")
```

### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes