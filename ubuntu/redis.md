# redis
centos7 下安装 redis

## Installation

编译和安装所需要的包
```
yum install gcc tcl
```

进入源码目录：
```
cd /usr/local/src
wget http://download.redis.io/releases/redis-4.0.2.tar.gz
tar xzf redis-4.0.2.tar.gz
cd redis-4.0.2
```

安装(安装在/usr/local/bin目录下)
```
make PREFIX=/usr/local/redis install
```


## service
将Redis注册成服务

拷贝Redis启动脚本复制到/etc/rc.d/init.d/目录下，并命名为 redis
```
cp /usr/local/src/redis-4.0.2/utils/redis_init_script /etc/rc.d/init.d/redis
```

编辑/etc/rc.d/init.d/redis
```
#chkconfig: 2345 80 90
```

将配置文件 `/usr/local/src/redis-4.0.2/redis.conf` 复制到 `/etc/redis` 并重命名为`6379.conf`
```
cp /usr/local/src/redis-4.0.2/redis.conf /etc/redis/6379.conf 
```

以上配置完成后
```
chkconfig --add redis
```

## config
修改配置 `/etc/redis/6379.conf`
```
daemonize no > daemonize yes
appendonly no > appendonly yes
bind 127.0.0.1 > ##bind 127.0.0.1
```

## firewall-cmd
```
firewall-cmd --permanent --zone=trusted --add-port=6379/tcp
firewall-cmd --reload
```

## command
```
service redis start
service redis stop
```

## ref
[Centos安装Redis - 简书](http://www.jianshu.com/p/cc1105cfb743)