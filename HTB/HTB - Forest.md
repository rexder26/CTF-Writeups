# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #activedirectory #ASREProasting 

# Findings

## External
### Enumeration
![](https://i.imgur.com/7iqDCM5.png)
- Anonymous RPC
	- ![](https://i.imgur.com/9rIjh0a.png)
- Filtered with grep and awk
	- ![](https://i.imgur.com/G0GEIvX.png)
- We got Asreproasting, changed with getnpuser
	- ![](https://i.imgur.com/hp6wIAI.png)
- ![](https://i.imgur.com/0VKSL5A.png)
` svc-alfresco : s3rvice `
### Gaining Access

![](https://i.imgur.com/sOLthpl.png)

## Internal
### Enumeration
```shell
if not exist "!amqpBrokerDir!" mkdir "!amqpBrokerDir!"
echo | set /p dummyName="amqp:#amqpUsername#:#amqpPassword#@!brokerAddr!:5672/reactiveRequestAmqpQueueId" > "!amqpBrokerDir!/uri_amqp.txt"
echo | set /p dummyName="tunnel:agentId1:bogus@localhost:6672/reactiveRequestAmqpQueueId" > "!amqpBrokerDir!/uri_tunnel.txt"
```

#amqpPassword#@!brokerAddr!
### Gaining Access


### Maintaining Access


# Random Notes