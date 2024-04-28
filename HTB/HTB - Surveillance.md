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
`$enum$`

### Gaining Access


## Internal
### Enumeration
`$enum$`

### Gaining Access


### Maintaining Access


# Random Notes
![](https://i.imgur.com/dkr8zPh.png)
![](https://i.imgur.com/yozKpDB.png)

![](https://i.imgur.com/qoYcdPK.png)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
    <system.webServer>
         <rewrite>
             <rules>
                <rule name="Rewrite" stopProcessing="true">
                    <match url="(.+)" ignoreCase="false" />
                    <conditions logicalGrouping="MatchAll">
	                    # This condition checks if the requested URL does not match an existing file
                        <add input="{REQUEST_FILENAME}" matchType="IsFile" ignoreCase="false" negate="true" />
                        # This condition checks if the requested URL does not match an existing directory
                        <add input="{REQUEST_FILENAME}" matchType="IsDirectory" ignoreCase="false" negate="true" />
                        # This condition checks if the requested URL does not match the pattern specified. In this case, it checks if the URL does not start with `/favicon.ico` or `/apple-touch-icon` followed by any characters and ending with `.png`.
                        <add input="{URL}" pattern="^/(favicon\.ico|apple-touch-icon.*\.png)$" negate="true" />
                    </conditions>
                    <action type="Rewrite" url="index.php?p={R:1}" appendQueryString="true" />
                </rule>
             </rules>
         </rewrite>
        <urlCompression doStaticCompression="true" doDynamicCompression="true" />
        <defaultDocument>
            <files>
                <clear />
                <add value="index.php" />
                <add value="index.htm" />
                <add value="index.html" />
            </files>
        </defaultDocument>
    </system.webServer>
</configuration>
```
![](https://i.imgur.com/gSdsLs2.png)
![](https://i.imgur.com/UqTzpw0.png)
# privilege escalation
- [ ] /var/www/html/craft/storage/logs/web-2024-04-10.log
- [ ] /var/www/html/craft/vendor/defuse/php-encryption/src/File.php
- [ ] /var/www/html/craft/vendor/composer/autoload_static.ph
- [ ] /var/www/html/craft/vendor/defuse/php-encryption/src/Crypto.php
- [ ] /var/www/html/craft/vendor/seld/cli-prompt/src/CliPrompt.php
- [ ] /var/www/html/craft/vendor/craftcms/cms/src/controllers/InstallController.php
- [ ] /var/www/html/craft/vendor/craftcms/cms/src/db/Connection.php
- [ ] /var/www/html/craft/vendor/craftcms/cms/src/db/mysql/Schema.php
- [ ] /var/www/html/craft/vendor/craftcms/cms/src/elements/User.php
- [ ] /var/www/html/craft/vendor/craftcms/cms/src/translations/en-GB/var/www/html/craft/vendor/craftcms/cms/src/web/assets/d3/dist/d3.js
- [x]   - Potential Password 'CraftCMSPassword2023!' (/var/www/html/craft/.env:19)
- [ ] /var/www/html/craft/web/bash.sh
/var/www/html/craft/vendor/paragonie/random_compat/build-phar.sh
/var/www/html/craft/vendor/craftcms/server-check/check.sh
- /etc/ImageMagick-6/mime.xml
- /var/www/html/craft/templates/home/_entry.twig

![](https://i.imgur.com/nbK92sp.png)
`craftuser:CraftCMSPassword2023!`
![](https://i.imgur.com/gbKKOED.png)
- mysql is on!
- ![](https://i.imgur.com/wofJngh.png)- `admin : $2y$13$FoVGcLXXNe81B6x9bKry9OzGSSIYL7/ObcmQ0CXtgw.EpuNcx8tGe`
- users 
	- `matthew : starcraft122490
	- zoneminder`
- ![](https://i.imgur.com/xkIgUqP.png)
- Cracked the hash
	- ![](https://i.imgur.com/QLhqpUp.png)


```shell
╔══════════╣ Analyzing Backup Manager Files (limit 70)
-rw-r--r-- 1 root zoneminder 5265 Nov 18  2022 /usr/share/zoneminder/www/ajax/modals/storage.php
-rw-r--r-- 1 root zoneminder 1249 Nov 18  2022 /usr/share/zoneminder/www/includes/actions/storage.php

-rw-r--r-- 1 root zoneminder 3503 Oct 17 11:32 /usr/share/zoneminder/www/api/app/Config/database.php
		'password' => ZM_DB_PASS,
		'database' => ZM_DB_NAME,
		'host' => 'localhost',
		'password' => 'ZoneMinderPassword2023',
		'database' => 'zm',
				$this->default['host'] = $array[0];
			$this->default['host'] = ZM_DB_HOST;
-rw-r--r-- 1 root zoneminder 11257 Nov 18  2022 /usr/share/zoneminder/www/includes/database.php
```

![](https://i.imgur.com/J5KPwRo.png)
```c
server {
    listen 127.0.0.1:8080;

    root /usr/share/zoneminder/www;

    index index.php;

    access_log /var/log/zm/access.log;
    error_log /var/log/zm/error.log;

    location / {
        try_files $uri $uri/ /index.php?$args =404;

        location ~ /api/(css|img|ico) {
            rewrite ^/api(.+)$ /api/app/webroot/$1 break;
            try_files $uri $uri/ =404;
        }
        location /api {
            rewrite ^/api(.+)$ /api/app/webroot/index.php?p=$1 last;
        }
        location /cgi-bin {
            include fastcgi_params;

            fastcgi_param SCRIPT_FILENAME $request_filename;
            fastcgi_param HTTP_PROXY "";

            fastcgi_pass unix:/run/fcgiwrap.sock;
        }

        location ~ \.php$ {
            include fastcgi_params;

            fastcgi_param SCRIPT_FILENAME $request_filename;
            fastcgi_param HTTP_PROXY "";

            fastcgi_index index.php;

            fastcgi_pass unix:/var/run/php/php8.1-fpm-zoneminder.sock;
        }
    }
}
```
![](https://i.imgur.com/JdBBD3x.png)
- [ ] includes/auth.php
- [ ] includes/User.ph
- [ ] includes/Monitor.php
- [ ] includes/actions/user.php
- [ ] api/lib/Cake/Console/Templates/skel/Config/email.php.default
- [ ] api/lib/Cake/Model/Datasource/Database/Mysql.php
- [ ] api/lib/Cake/Test/Fixture/UserFixture.php
- [ ] api/lib/Cake/Test/Fixture/CallbackFixture.php
- [ ] api/lib/Cake/Test/Case/Model/Datasource/Database/PostgresTest.php
- [ ] api/lib/Cake/Test/Case/Controller/Component/AuthComponentTest.php:1124:		$this->Auth->login(array('username' => 'admad', 'password' => 'cake'));
- [ ] api/lib/Cake/Test/Case/Utility/DebuggerTest.php:606:			'password' => 'cakephp-password',
- [ ] api/lib/Cake/Network/Http/HttpSocket.php:499: *     'password' => 'bruce_w4yne'
- [ ] api/app/Config/database.php


` Configure::write('Security.salt', 'f5fUKI1Nsp0vKmiobQuu0nCiCGYte');ls
`
- Port 8080 is open locally
	- ![](https://i.imgur.com/DZ3qIye.png)
- I did port forwarding
	- ![](https://i.imgur.com/sronEwP.png)
![](https://i.imgur.com/qKOusOk.png)
https://github.com/rvizx/CVE-2023-26035

![](https://i.imgur.com/j4gcZ03.png)
- coudnt read the file so i sent it to /tmp
- ![](https://i.imgur.com/0BoZFqb.png)
```shell

/usr/bin/zmaudit.pl    /usr/bin/zmfilter.pl         /usr/bin/zmrecover.pl    /usr/bin/zmtrack.pl    /usr/bin/zmwatch.pl
/usr/bin/zmcamtool.pl  /usr/bin/zmonvif-probe.pl    /usr/bin/zmstats.pl      /usr/bin/zmtrigger.pl  /usr/bin/zmx10.pl
/usr/bin/zmcontrol.pl  /usr/bin/zmonvif-trigger.pl  /usr/bin/zmsystemctl.pl  /usr/bin/zmupdate.pl
/usr/bin/zmdc.pl       /usr/bin/zmpkg.pl            /usr/bin/zmtelemetry.pl  /usr/bin/zmvideo.pl privelege escalation


```

![](https://i.imgur.com/AEDUMZO.png)
![](https://i.imgur.com/kVCH0XX.png)
