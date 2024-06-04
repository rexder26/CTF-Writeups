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
![](https://i.imgur.com/9XytqfR.png)

- STOPPED
```shell
rexder@HunterMachine /o/ysoserial [70]> sudo java -jar /opt/ysoserial/ysoserial-master.jar CommonsCollections3 calca.exe
Error while generating or serializing payload
java.lang.IllegalAccessError: class ysoserial.payloads.util.Gadgets (in unnamed module @0x1c685b6) cannot access class com.sun.org.apache.xalan.internal.xsltc.trax.TemplatesImpl (in module java.xml) because module java.xml does not export com.sun.org.apache.xalan.internal.xsltc.trax to unnamed module @0x1c685b6
	at ysoserial.payloads.util.Gadgets.createTemplatesImpl(Gadgets.java:102)
	at ysoserial.payloads.CommonsCollections3.getObject(CommonsCollections3.java:36)
	at ysoserial.GeneratePayload.main(GeneratePayload.java:34)
```
- it is not working on my machine, but all the writeups's workes good
### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes