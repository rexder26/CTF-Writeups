3- 10.149.12.62
- SIEM : ` Natanhailu82 : Hackyou@123 `
- AF: ` tube_team : yaIbLFq|IVxJL2mDoKnH `


Links
- Wiki: https://wiki.tube.stf/start
- Tube: https://wiki.tube.stf/blueteam4:start#%D1%81%D0%B4%D0%B0%D1%87%D0%B0_%D0%BE%D1%82%D1%87%D0%B5%D1%82%D0%BE%D0%B2

- Infrastructure 
![](https://i.imgur.com/YCnoUiO.png)

```shell

# SIEM
(correlation_name != null) AND (event_src.host ="10.149.12.133")

body contains "extmet"


# NAD
src.ip == 10.119.11.165 && dst.ip == 10.119.11.165



# FILES 

extmet
chmod +x /var/tmp/dt

C:\\Program Files\\Automiq\\Alpha.Security\\alpha.security.agent.exe"
```