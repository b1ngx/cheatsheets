# Redis
centos7 下安装 redis

## Install

install the CentOS Development Tools, which are used to allow you to build and compile software from source code.

```
yum -y groupinstall development
```

进入源码目录：

```
cd /opt
wget http://download.redis.io/releases/redis-4.0.6.tar.gz
tar xzvf redis-4.0.6.tar.gz
cd redis-4.0.6
```

安装(安装在/usr/local/bin目录下)

```
make
make test
make install
```


## Service
将Redis注册成服务

```
./utils/install_server.sh
```

按提示操作，安装完成

```
Welcome to the redis service installer
This script will help you easily set up a running redis server

Please select the redis port for this instance: [6379]
Selecting default: 6379
Please select the redis config file name [/etc/redis/6379.conf]
Selected default - /etc/redis/6379.conf
Please select the redis log file name [/var/log/redis_6379.log]
Selected default - /var/log/redis_6379.log
Please select the data directory for this instance [/var/lib/redis/6379]
Selected default - /var/lib/redis/6379
Please select the redis executable path [/usr/local/bin/redis-server]
Selected config:
Port           : 6379
Config file    : /etc/redis/6379.conf
Log file       : /var/log/redis_6379.log
Data dir       : /var/lib/redis/6379
Executable     : /usr/local/bin/redis-server
Cli Executable : /usr/local/bin/redis-cli
Is this ok? Then press ENTER to go on or Ctrl-C to abort.
Copied /tmp/6379.conf => /etc/init.d/redis_6379
Installing service...
Successfully added to chkconfig!
Successfully added to runlevels 345!
Starting Redis server...
Installation successful!
```


## Config
修改配置 `/etc/redis/6379.conf`

```
daemonize no > daemonize yes
appendonly no > appendonly yes
bind 127.0.0.1 > #bind 127.0.0.1
```

## Command
服务

```
#文件启动
/etc/init.d/redis_6379 status/start/stop

#服务启动
service redis status/start/stop
```

常用命令

```
#验证连接
PING

#远程连接
redis-cli -h [host] -p [port] -a [password]

#认证
AUTH password

#选择 db
SELECT [number]

#清空数据
FLUSHDB
FLUSHALL

# 返回有序集合中 score 在指定区间，并降序排列的集合
ZREVRANGEBYSCORE toutiao_views +inf -inf LIMIT 0 5

```

认证密码
 
 ```
 # 修改配置完文件，将密码设置为 secret_password
 requirepass secret_password
 
 # 或者通过命令
 CONFIG SET requirepass secret_password
 QUIT
 AUTH secret_password
 ```
 
## Ref
[Redis Install](https://realguess.net/2014/07/19/non-interactive-redis-install/)
[Redis 教程](http://www.runoob.com/redis/redis-tutorial.html)

