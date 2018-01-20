# mysql

## 安装
1. 访问下载页面 `https://dev.mysql.com/downloads/repo/yum/`
2. 下载 `https://dev.mysql.com/get/mysql57-community-release-el7-11.noarch.rpm`
3. 安装 package: `rpm -ivh mysql57-community-release-el7-11.noarch.rpm`
4. 安装 MySQL server: `yum install mysql-server`

## 配置

- 配置文件：/etc/my.cnf
- 日志文件：/var/log/mysqld.log
- 服务启动脚本：/usr/lib/systemd/system/mysqld.service
- socket文件：/var/run/mysqld/mysqld.pid

## 命令

系统命令

```
systemctl start mysqld
systemctl status mysqld
```

mysql

```
mysql --help
mysql -u root -p
mysql -h [host/ip] -P [port] -u [user] -p [password]
```

## 权限管理

查看权限

```
mysql> show grants;
+------------------------------------------------------------+
| Grants for sam@%                                           |
+------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'sam'@'%' WITH GRANT OPTION |
+------------------------------------------------------------+
1 row in set (0.00 sec)
```

查看某个用户的权限：

```
mysql> show grants for 'sam';
+------------------------------------------------------------+
| Grants for sam@%                                           |
+------------------------------------------------------------+
| GRANT ALL PRIVILEGES ON *.* TO 'sam'@'%' WITH GRANT OPTION |
+------------------------------------------------------------+
1 row in set (0.00 sec)
```

刷新权限

```
flush privileges;
```

添加权限

```
grant all privileges on *.* to sam@'localhost' identified by "password" with grant option;
```

命令说明

- `ALL PRIVILEGES` 是表示所有权限，你也可以使用 `select、update` 等权限。
- `ON` 用来指定权限针对哪些库和表。
- `*.*` 中前面的*号用来指定数据库名，后面的*号用来指定表名。
- `TO` 表示将权限赋予某个用户。
- `sam@'localhost'` 表示 sam 用户，@后面接限制的主机，可以是IP、IP段、域名以及%，%表示任何地方。注意：这里%有的版本不包括本地，以前碰到过给某个用户设置了%允许任何地方登录，但是在本地登录不了，这个和版本有关系，遇到这个问题再加一个localhost的用户就可以了。
- `IDENTIFIED BY` 指定用户的登录密码。
- `WITH GRANT OPTION` 这个选项表示该用户可以将自己拥有的权限授权给别人。注意：经常有人在创建操作用户的时候不指定WITH GRANT OPTION选项导致后来该用户不能使用GRANT命令创建用户或者给其它用户授权。

>可以使用GRANT重复给用户添加权限，权限叠加，比如你先给用户添加一个select权限，然后又给用户添加一个insert权限，那么该用户就同时拥有了select和insert权限。

## mariadb

## ref

[MySQL5.7安装与配置](http://blog.csdn.net/xyang81/article/details/51759200)
[How To Install MySQL on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-centos-7)
[MySQL之权限管理](https://www.cnblogs.com/Richardzhu/p/3318595.html)

