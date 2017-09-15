# mysql

## install


## config

- 配置文件：/etc/my.cnf
- 日志文件：/var/log/mysqld.log
- 服务启动脚本：/usr/lib/systemd/system/mysqld.service
- socket文件：/var/run/mysqld/mysqld.pid

## iptables

```
//查看规则
iptables --list-rule

// 添加规则
iptables -I INPUT -p tcp -m tcp --dport 3306 -j ACCEPT

// 删除 INPUR 第 1 条规则
iptables -D INPUT 1
```

## ref

[MySQL5.7安装与配置](http://blog.csdn.net/xyang81/article/details/51759200)
