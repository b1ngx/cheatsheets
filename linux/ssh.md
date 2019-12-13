# ssh

## ssh-keygen

**-f** : specify a different name for your key pair

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

## proxy

```
ssh root@host -o "ProxyCommand=nc -X 5 -x 127.0.0.1:7891 %h %p"
```


