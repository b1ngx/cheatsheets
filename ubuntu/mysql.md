# mysql

## Install


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

//Disable firewalld by the following command:
systemctl disable firewalld

//Then install iptables-service by following command:
yum install iptables-services

//Then enable iptables as services:
systemctl enable iptables

//Now you can save your iptable rules by following command:
service iptables save
```

## Firewall Rules
```
// 查看
firewall-cmd --permanent --zone=trusted --list-sources
firewall-cmd --permanent --zone=trusted --list-ports
// add 子网掩码 225.225.252.0 port=3306
firewall-cmd --permanent --zone=trusted --add-source=192.168.0.0/22
firewall-cmd --permanent --zone=trusted --add-port=3306/tcp
firewall-cmd --reload
// remove
firewall-cmd --permanent --zone=trusted --remove-source=192.168.0.0/22
firewall-cmd --permanent --zone=trusted --remove-port=3306/tcp
```

## ref

[MySQL5.7安装与配置](http://blog.csdn.net/xyang81/article/details/51759200)


