# 防火墙

iptables 和 firewall-cmd


## 系统命令

#### iptables

```
service iptable status/stop/start
chkconfig iptables off
```

#### firewall-cmd

```
firewall-cmd --state
systemctl status firewalld
```

## 配置
#### iptables

```
//查看规则
iptables --list-rule

// 添加 mysql 3306 规则
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

#### firewall Rules

查看端口

```
firewall-cmd --permanent --zone=trusted --list-sources
firewall-cmd --permanent --zone=trusted --list-ports
```

设置规则

```
# 添加子网掩码为 225.225.252.0 port=3306
firewall-cmd --permanent --zone=trusted --add-source=192.168.0.0/22
firewall-cmd --permanent --zone=trusted --add-port=3306/tcp
firewall-cmd --reload
```
删除规则

```
firewall-cmd --permanent --zone=trusted --remove-source=192.168.0.0/22
firewall-cmd --permanent --zone=trusted --remove-port=3306/tcp
```

redis

```
# 防火墙开放 6379 端口
firewall-cmd --permanent --zone=trusted --add-port=6379/tcp
firewall-cmd --reload
```

