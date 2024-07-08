# Information
- CTF Name: Dante
- CTF Level: Level I
- CTF Description: 
- Date: 21, June 2024
- Platform: HTB
- Category: Prolab
- IP: **10.10.110.0/24**

```shell
# Opened Ports For for
-> 1002 is not used
```
# Findings
### Credentials
- ` james : Toyota `
- `balthazar : TheJoker12345!`

### Owned Machines
1. [[Dante - WS01]] - No double Host
2. [[Dante - WS02]]
3. [[Dante - WS03]] - No double Host
4. [[Dante - NIX01 (FootHold)]]
5. [[Dante - NIX02]] - No double Host
6. [[Dante - NIX03]]
7. [[Dante - NIX04]]
8. [[Dante - NIX07]]
9. [[Dante - SQL01]]
10. [[Dante - DC01]] - **double** Host -> weird way
11. [[Dante - DC02]]
12. [[Dante - NIX05]]
13. [[Dante - NIX06]]
14. .
### Flags
1. `DANTE{Y0u_Cant_G3t_at_m3_br0!}`
2. `DANTE{j4m3s_NEEd5_a_p455w0rd_M4n4ger!}`
3. `DANTE{Too_much_Pr1v!!!!}`
4. `DANTE{Ther3s_M0r3_to_pwn_so_k33p_searching!}`
5. `DANTE{l355_t4lk_m04r_l15tening}`
6. `DANTE{Bad_pr4ct1ces_Thru_strncmp}`
7. `DANTE{U_M4y_Kiss_Th3_Br1d3}`
8. `DANTE{D0nt_M3ss_With_MinatoTW}`
9. `DANTE{LF1_M@K3s_u5_lol}`
10. `DANTE{L0v3_m3_S0m3_H1J4CK1NG_XD}`
11. `DANTE{SH4RKS_4R3_3V3RYWHERE}`
12. `DANTE{wHy_y0U_n0_s3cURe?!?!}`
13. `DANTE{Pretty_Horrific_PH4IL!}`
14. `DANTE{sudo_M4k3_me_@_Sandwich}`
15. `DANTE{Feel1ng_Blu3_or_Zer0_f33lings?}`
16. `DANTE{1_jusT_c@nt_st0p_d0ing_th1s}`
17. `DANTE{superB4d_p4ssw0rd_FTW}`
18. `DANTE{Qu0t3_I_4M_secure!_unQu0t3}`
19. `DANTE{Im_too_hot_Im_K3rb3r045TinG!}`
20. `DANTE{DC_or_Marvel?}`
21. `DANTE{to_g0_4ward_y0u_mus7_g0_back}`
22. `DANTE{g0tta_<3_ins3cur3_GROupz!}`
23. `DANTE{0verfl0wing_l1k3_craz33!}`
24. `DANTE{H1ding_1n_th3_c0rner}`
25. `DANTE{Alw4ys_check_th053_group5}`
26. `DANTE{Mult1ple_w4Ys_in!}`
27. .

### Vulns
1. Information Disclosure - `http://dante.htb:65000/robots.txt`
2. Path Disclosure - `http://dante.htb:65000/wordpress/wp-content/debug.log`
	1. ![](https://i.imgur.com/SikedVO.png)
3. Sensitive Data leak - `http://dante.htb:65000/wordpress/.wp-config.php.swp`
4. RPC enabled
	1. ![](https://i.imgur.com/gzkdloh.png)

## External
### Enumeration
![](https://i.imgur.com/t5bnm7B.png)
- Target is `10.10.110.100` the `.2` is Out-of-scope.
![](https://i.imgur.com/unbYlyg.png)
![](https://i.imgur.com/nDR8UNB.png)
![](https://i.imgur.com/XOxxwpq.png)
```shell

# There is Header "DANTE-WEB-NIX01"

define( 'DB_NAME', 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'shaun' );

/** MySQL database password */
define( 'DB_PASSWORD', 'password' );

/** MySQL hostname */
define( 'DB_HOST', 'localhost' );

/** Database Charset to use in creating database tables. */
define( 'DB_CHARSET', 'utf8mb4' );
```
![](https://i.imgur.com/mxGxsVU.png)
```shell
- Finalize Wordpress permission changes - PENDING
- Update links to to utilize DNS Name prior to changing to port 80 - PENDING
- Remove LFI vuln from the other site - PENDING
- Reset James' password to something more secure - PENDING
- Harden the system prior to the Junior Pen Tester assessment - IN PROGRESS
```
https://gist.github.com/LukaSikic/48f30805b10e2a4dfd6858ebdb304be9
```shell
[i] Plugin(s) Identified:

[+] akismet
 | Location: http://dante.htb:65000/wordpress/wp-content/plugins/akismet/
 | Last Updated: 2024-05-31T16:57:00.000Z
 | Readme: http://dante.htb:65000/wordpress/wp-content/plugins/akismet/readme.txt
 | [!] The version is out of date, the latest version is 5.3.2
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://dante.htb:65000/wordpress/wp-content/plugins/akismet/, status: 200
 |
 | Version: 4.1.5 (100% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://dante.htb:65000/wordpress/wp-content/plugins/akismet/readme.txt
 | Confirmed By: Readme - ChangeLog Section (Aggressive Detection)
 |  - http://dante.htb:65000/wordpress/wp-content/plugins/akismet/readme.txt

[+] custom-fields-gutenberg
 | Location: http://dante.htb:65000/wordpress/wp-content/plugins/custom-fields-gutenberg/
 | Latest Version: 2.4
 | Last Updated: 2024-06-18T22:54:00.000Z
 |
 | Found By: Known Locations (Aggressive Detection)
 |  - http://dante.htb:65000/wordpress/wp-content/plugins/custom-fields-gutenberg/, status: 403
 |
 | The version could not be determined.
```
- I did all i can and there is nothing left except Bruteforce. After Lot of Hour BruteForce i got the password.
![](https://i.imgur.com/tnzWKFp.png)
### Gaining Access
- Wordpress RCE
![](https://i.imgur.com/CAGkWYC.png)
- By using the James Password Again i got to the james user.
## Internal
### Enumeration
![](https://i.imgur.com/ReZyhKr.png)
```

/etc/ssh

-rw-r--r-- 1 root root 12288 Aug  4  2021 /var/www/html/wordpress.bak/.wp-config.php.swp
-rw-r--r-- 1 root root 12288 Dec  3  2020 /var/www/html/wordpress/.wp-config.php.swp
/root/flag.txt
```
![](https://i.imgur.com/L8A6HGq.png)
![](https://i.imgur.com/8GDuRmj.png)
### Gaining Access
![](https://i.imgur.com/rRN8Nda.png)
### Maintaining Access
![](https://i.imgur.com/qGR4pZo.png)
```sh
# IP
172.16.1.20,5,19,10,12,17,13,101,102
172.16.1.5
172.16.1.19
172.16.1.10
172.16.1.12
172.16.1.17
172.16.1.13
172.16.1.100   <- Mine
172.16.1.101
172.16.1.102
```
![](https://i.imgur.com/8N0gJvz.png)
# Random Notes
```sh
    "widget_text[2]": {
        "starter_content": true,
        "value": {
            "encoded_serialized_instance": "YTo0OntzOjU6InRpdGxlIjtzOjE1OiJBYm91dCBUaGlzIFNpdGUiO3M6NDoidGV4dCI7czo4NToiVGhpcyBtYXkgYmUgYSBnb29kIHBsYWNlIHRvIGludHJvZHVjZSB5b3Vyc2VsZiBhbmQgeW91ciBzaXRlIG9yIGluY2x1ZGUgc29tZSBjcmVkaXRzLiI7czo2OiJmaWx0ZXIiO2I6MTtzOjY6InZpc3VhbCI7YjoxO30=",
            "title": "About This Site",
            "is_widget_customizer_js_value": true,
            "instance_hash_key": "ade885ebb0d120cf056cc13787bf3052"
        },
        "type": "option",
        "user_id": 1,
        "date_modified_gmt": "2020-05-09 21:16:47"
    },
    "sidebars_widgets[sidebar-1]": {
        "starter_content": true,
        "value": [
            "text-2"
        ],
        "type": "option",
        "user_id": 1,
        "date_modified_gmt": "2020-05-09 21:16:47"
    },
    "widget_text[3]": {
        "starter_content": true,
        "value": {
            "encoded_serialized_instance": "YTo0OntzOjU6InRpdGxlIjtzOjc6IkZpbmQgVXMiO3M6NDoidGV4dCI7czoxNjg6IjxzdHJvbmc+QWRkcmVzczwvc3Ryb25nPgoxMjMgTWFpbiBTdHJlZXQKTmV3IFlvcmssIE5ZIDEwMDAxCgo8c3Ryb25nPkhvdXJzPC9zdHJvbmc+Ck1vbmRheSZuZGFzaDtGcmlkYXk6IDk6MDBBTSZuZGFzaDs1OjAwUE0KU2F0dXJkYXkgJmFtcDsgU3VuZGF5OiAxMTowMEFNJm5kYXNoOzM6MDBQTSI7czo2OiJmaWx0ZXIiO2I6MTtzOjY6InZpc3VhbCI7YjoxO30=",
            "title": "Find Us",
            "is_widget_customizer_js_value": true,
            "instance_hash_key": "e706c7ed0fe2203c88470e5731d58578"
        },
        "type": "option",
        "user_id": 1,
        "date_modified_gmt": "2020-05-09 21:16:47"
    },
```