# Information
- CTF Name: Devvotex
- CTF Level: Easy
- CTF Description: 
- Date: 4/4/2024
- Platform: 
- Category: #vhost #joomla

# Findings

## External
### Enumeration
- As Always I started with my Nmap Scan gave me 4 ports those are open.
	- ![](https://i.imgur.com/ytIIx9g.png)
- Tried to access and enumrate The main domain But there werent anything, so i went to subdomain enumration i got nothing there, Finally on **VHOST** enumration i got a domain `dev.devvortex.htb`.
	- ![](https://i.imgur.com/nXo86Zu.png)
- Thist Vhost was a joomla Web, i got that information from Wapplayzer Broweser extension and also, the `robot.txt` file on the server.
	- ![](https://i.imgur.com/ujRytoE.png)
- As soon as i knew it it Joomla, I tried to enumerate it with tool called `joomscan`. and i Found that the joomla Installed on the server is old and vulnerable.
	- It is `Joomla 4.2.6`![](https://i.imgur.com/LAu717k.png)
### Gaining Access
- I tested the server with Different Exploits of joomla 4.2.6, some of them werent working as you see.
![](https://i.imgur.com/sjT3VNe.png)
- but finally i got one [Exploit](https://github.com/ThatNotEasy/CVE-2023-23752)
	- ![](https://i.imgur.com/GXn48xU.png)
![](https://i.imgur.com/jFZTgGx.png)
- It worked and gave me a Credentials for the user lewis.
## Internal
### Enumeration
- The Credentials we got on the External Process was not used to access the server using ssh(i knew that after trying lol), 
	- Then After i tried it on the joomla admin login page.
### Gaining Access
- The username and password we got worked on the joomla login page.
	- ![](https://i.imgur.com/tyiVTXk.png)
- On this step what i did is just trying to upload some php shell because previously i have played some CTFs that have this kinda COntent manangement system andi got privillge with php shell.
	- ![](https://i.imgur.com/WG0RMtA.png)
	- ![](https://i.imgur.com/LYQ5Dvw.png)
- I uploaded a php shell that i got from [Pentest Monkey](https://github.com/pentestmonkey/php-reverse-shell/blob/master/php-reverse-shell.php)
- Then i started my listener 
	- ![](https://i.imgur.com/Qjny64i.png)
- Then I tried to access the page i put my php payload.
	- ![](https://i.imgur.com/rza48u3.png)
- Boom we got shell
	- ![](https://i.imgur.com/77boUv9.png)
### Maintaining Access
- I tried Different Priv Esc techniques but non of them were working, But as you can see when we try to enumerate the network part, there is a listening port on `3306` and `33060`, by default `3306` is a mysql server port, so the another port is same but with `0` that was confusing,
	- ![](https://i.imgur.com/aWuWW5G.png)
- but i tried to access the mysql server, with lewis credentials. But it was not working.
	- ![](https://i.imgur.com/NJ9mrNR.png)
- after so many hours i remembered that I can use mysql server with another port, and as i remembered there is another port with `0` at the end, then i tried that
	- ![](https://i.imgur.com/gK9Xucy.png)
- We got the MySQL server cli, Then i tried to get Credentials, and Congratulations we got for the user `lewis` and `logan`.
	- ![](https://i.imgur.com/0fRNpl3.png)
- We have the lewis Credentials so, i tried to copy the logans Credentials and tried to Crack it with john, and Boom we got it!!!
	- ![](https://i.imgur.com/9OYivTu.png)
- Tried to ssh and we are IN!
	- ![](https://i.imgur.com/TxwAjbL.png)
- And We got the user flag (●'◡'●)
	- ![](https://i.imgur.com/f1t5LEa.png)
- Then Contined to get the root flag, So when i tried the `sudo -l` for any program that can be run with sudo and no password we got the `/usr/bin/apport-cli`
	- ![](https://i.imgur.com/4BLesk4.png)
- So i tried to Google how i can use this tool and do Privilege escalate.
	- ![](https://i.imgur.com/1Lp5BF9.png)
- and Got [This Exploit](https://diegojoelcondoriquispe.medium.com/cve-2023-1326-poc-c8f2a59d0e00)
	- ![](https://i.imgur.com/mJQprHQ.png)
- And BOOM BOOM BOOM, we are `root`
	- ![](https://i.imgur.com/bnr3Xk2.png)
Thank You ;)



# Random Notes

/media/templates/site/cassiopeia/assets/img/logo.pn

Disallow: /administrator/
Disallow: /api/
Disallow: /bin/
Disallow: /cache/
Disallow: /cli/
Disallow: /components/
Disallow: /includes/
Disallow: /installation/
Disallow: /language/
Disallow: /layouts/
Disallow: /libraries/
Disallow: /logs/
Disallow: /modules/
Disallow: /plugins/
Disallow: /tmp/






[+] Username          : lewis
[+] Password          : P4ntherg0t1n5r3c0n##

!
http://dev.devvortex.htb/templates/cassiopeia/error.php



/home/logan/.bash_history
/var/www/dev.devvortex.htb/libraries/web.config


/var/www/dev.devvortex.htb/administrator/logs

/var/www/dev.devvortex.htb/tmp

```shell
        <?php                                                     
class JConfig {                                          
        public $offline = false;                             
        public $offline_message = 'This site is down for maintenance.<br>Please check back again soon.';                            
        public $display_offline_message = 1;                 
        public $offline_image = '';                     
        public $sitename = 'Development';                  
        public $editor = 'tinymce';                       
        public $captcha = '0';                            
        public $list_limit = 20;                          
        public $access = 1;                             
        public $debug = false;                          
        public $debug_lang = false;                      
        public $debug_lang_const = true;                   
        public $dbtype = 'mysqli';                        
        public $host = 'localhost';                         
        public $user = 'lewis';
        public $password = 'P4ntherg0t1n5r3c0n##';
        public $db = 'joomla';
        public $dbprefix = 'sd4fg_';
        public $dbencryption = 0;
        public $dbsslverifyservercert = false;
        public $dbsslkey = '';
        public $dbsslcert = '';
        public $dbsslca = '';
        public $dbsslcipher = '';
        public $force_ssl = 0;
        public $live_site = '';
        public $secret = 'ZI7zLTbaGKliS9gq';
        public $gzip = false;
        public $error_reporting = 'default';
        public $helpurl = 'https://help.joomla.org/proxy?keyref=Help{major}{minor}:{keyref}&lang={langcode}';
        public $offset = 'UTC';
        public $mailonline = true;
        public $mailer = 'mail';
        public $mailfrom = 'lewis@devvortex.htb';
        public $fromname = 'Development';
        public $sendmail = '/usr/sbin/sendmail';
        public $smtpauth = false;
        public $smtpuser = '';
        public $smtppass = '';
        public $smtphost = 'localhost';
        public $smtpsecure = 'none';
        public $smtpport = 25;
        public $caching = 0;
        public $cache_handler = 'file';
        public $cachetime = 15;
        public $cache_platformprefix = false;
        public $MetaDesc = '';
        public $MetaAuthor = true;
        public $MetaVersion = false;
        public $robots = '';
        public $sef = true;
        public $sef_rewrite = false;
        public $sef_suffix = false;
        public $unicodeslugs = false;
        public $feed_limit = 10;
        public $feed_email = 'none';
        public $log_path = '/var/www/dev.devvortex.htb/administrator/logs';
        public $tmp_path = '/var/www/dev.devvortex.htb/tmp';
        public $lifetime = 15;
        public $session_handler = 'database';
        public $shared_session = false;
        public $session_metadata = true;
```
