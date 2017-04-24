# ssh

## ssh-keygen

`-f` : specify a different name for your key pair
```
ssh-keygen -f gitlab
```

## 问题

### [ssh “permissions are too open” error](http://stackoverflow.com/questions/9270734/ssh-permissions-are-too-open-error)

Keys need to be only readable by you:
```
chmod 400 ~/.ssh/id_rsa
```
edit: 600 appears to be fine as well (in fact better, per comment), have a peek at this article.

## ref
https://askubuntu.com/questions/306798/trying-to-do-ssh-authentication-with-key-files-server-refused-our-key
https://www.digitalocean.com/community/tutorials/how-to-protect-ssh-with-fail2ban-on-centos-7
