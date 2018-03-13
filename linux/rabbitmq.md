# RabbitMQ

## 安装 Erlang

To use Erlang 20.x on CentOS 7:

```
# In /etc/yum.repos.d/rabbitmq-erlang.repo
[rabbitmq-erlang]
name=rabbitmq-erlang
baseurl=https://dl.bintray.com/rabbitmq/rpm/erlang/20/el/7
gpgcheck=1
gpgkey=https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc
repo_gpgcheck=0
enabled=1
```

执行 `yum install erlang`

## 安装 RabbitMQ

```
wget https://dl.bintray.com/rabbitmq/all/rabbitmq-server/3.7.4/rabbitmq-server-3.7.4-1.el7.noarch.rpm

rpm --import https://dl.bintray.com/rabbitmq/Keys/rabbitmq-release-signing-key.asc

yum install rabbitmq-server-3.7.4-1.el7.noarch.rpm
```

#### 系统

```
systemctl enable rabbitmq-server.service
```

#### 管理

安装Web管理界面插件

```
rabbitmq-plugins enable rabbitmq_management
```

创建账号

```
rabbitmqctl add_user test 123456
```

设置用户角色

```
rabbitmqctl  set_user_tags  test  administrator
```

设置用户权限

```
rabbitmqctl set_permissions -p "/" test ".*" ".*" ".*"
```

设置完成后可以查看当前用户和角色(需要开启服务)

```
rabbitmqctl list_users
```

这时你就可以通过其他主机的访问RabbitMQ的Web管理界面了，浏览器输入：serverip:15672。

## 参考
- [Installing on RPM-based Linux (RHEL, CentOS, Fedora, openSUSE)](https://www.rabbitmq.com/install-rpm.html)
- [设置RabbitMQ远程ip登录](https://www.jianshu.com/p/e3af4cf97820)





