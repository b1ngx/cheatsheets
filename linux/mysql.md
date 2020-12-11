# mysql

## Get Started
安装
```
sudo apt update
sudo apt install mysql-server
sudo mysql_secure_installation
```

创建用户
```
CREATE USER 'username'@'host' IDENTIFIED WITH authentication_plugin BY 'password';
ALTER USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
省略 `authentication_plugin`，默认的加密插件为 `aching_sha2_password`

## Grant Privileges
```
GRANT PRIVILEGE ON database.table TO 'username'@'host';
GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

命令说明

- `ALL PRIVILEGES` 是表示所有权限，你也可以使用 `select、update` 等权限。
- `ON` 用来指定权限针对哪些库和表。
- `*.*` 中前面的*号用来指定数据库名，后面的*号用来指定表名。
- `TO` 表示将权限赋予某个用户。
- `username@'localhost'` 表示 username 用户，@后面接限制的主机，可以是IP、IP段、域名以及%，%表示任何地方。注意：这里%有的版本不包括本地，以前碰到过给某个用户设置了%允许任何地方登录，但是在本地登录不了，这个和版本有关系，遇到这个问题再加一个localhost的用户就可以了。
- `IDENTIFIED BY` 指定用户的登录密码。
- `WITH GRANT OPTION` 这个选项表示该用户可以将自己拥有的权限授权给别人。注意：经常有人在创建操作用户的时候不指定WITH GRANT OPTION选项导致后来该用户不能使用GRANT命令创建用户或者给其它用户授权。

>可以使用GRANT重复给用户添加权限，权限叠加，比如你先给用户添加一个select权限，然后又给用户添加一个insert权限，那么该用户就同时拥有了select和insert权限。

## QA

MySQL won't start - error: su: warning: cannot change directory to /nonexistent: No such file or directory.
```
sudo service mysql stop
sudo usermod -d /var/lib/mysql/ mysql
sudo service mysql start
```
https://stackoverflow.com/questions/62987154/mysql-wont-start-error-su-warning-cannot-change-directory-to-nonexistent

## Ref

- [MySQL之权限管理](https://www.cnblogs.com/Richardzhu/p/3318595.html)
- [Install MySQL on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04)
- [在 Ubuntu 上安装 MySQL](https://blog.csdn.net/liang19890820/article/details/105071479)
- [Navicat Premium 15](https://www.skyfinder.cc/2020/01/12/database-navicat-premium15/)
