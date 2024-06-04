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
![](https://i.imgur.com/V9kpYcb.png)
```shell
5080/tcp open  http    syn-ack nginx
|_http-favicon: Unknown favicon MD5: F7E3D97F404E71D302B3239EEF48D5F2
| http-title: Sign in \xC2\xB7 GitLab
|_Requested resource was http://ready.htb:5080/users/sign_in
| http-methods:
|_  Supported Methods: GET HEAD POST OPTIONS
| http-robots.txt: 53 disallowed entries (40 shown)
| / /autocomplete/users /search /api /admin /profile
| /dashboard /projects/new /groups/new /groups/*/edit /users /help
| /s/ /snippets/new /snippets/*/edit /snippets/*/raw
| /*/*.git /*/*/fork/new /*/*/repository/archive* /*/*/activity
| /*/*/new /*/*/edit /*/*/raw /*/*/blame /*/*/commits/*/*
| /*/*/commit/*.patch /*/*/commit/*.diff /*/*/compare /*/*/branches/new
| /*/*/tags/new /*/*/network /*/*/graphs /*/*/milestones/new
| /*/*/milestones/*/edit /*/*/issues/new /*/*/issues/*/edit
| /*/*/merge_requests/new /*/*/merge_requests/*.patch
|_/*/*/merge_requests/*.diff /*/*/merge_requests/*/edit
|_http-trane-info: Problem with XML parsing of /evox/about
```
![](https://i.imgur.com/6Yh0pcZ.png)
```shell
$databases = array (
  'default' =>
  array (
    'default' =>
    array (
      'database' => 'drupal',
      'username' => 'drupaluser',
      'password' => '%%cHzhNC=k9yYN!T',
      'host' => 'localhost',
      'port' => '',
      'driver' => 'mysql',
      'prefix' => '',
    ),
  ),
);
```
### Gaining Access
- Got the version of the gitlab and i googled or the effective exploit and i got this https://github.com/dotPY-hax/gitlab_RCE
![](https://i.imgur.com/IrqBEV1.png)
## Internal
### Enumeration
```
git@gitlab.example.com:/var/opt/gitlab/gitlab-rails/working$ cat /root_pass
YG65407Bjqvv9A0a8Tm_7w
```
![](https://i.imgur.com/zyhHcV6.png)
- Nothing over here
	- ![](https://i.imgur.com/OC3hipr.png)
![](https://i.imgur.com/EXkIhZ6.png)
- ` root : wW59U!ZKMbG9+*#h `
### Gaining Access


### Maintaining Access


# Random Notes