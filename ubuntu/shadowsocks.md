# shadowsocks

## 安装
```
pip install shadowsocks
```

## 配置

客户端

```
{
      "server": "187.188.189.190",
      "server_port": 8388,
      "password": "********",
      "method": "aes-256-cfb"
}

```

服务端

```
{
    "server": "187.188.189.190",
    "local_address": "127.0.0.1",
    "local_port": 1080,
    "port_password":{
        "8388": "password"
    },
    "timeout": 300,
    "method": "aes-256-cfb",
    "fast_open": true
}

```

## 命令

服务端

```
ssserver -c 配置文件 -d start/stop/restart
ssserver -c /etc/shadowsocks.json -d restart
```

客户端

```
sslocal -c /home/b1ng/ss.json -d start
sslocal -c 配置文件 -d start/stop/restart
```

## 开机启动

安装 `supervisor`

```
sudo apt install supervisor
```

编辑文件 `/etc/supervisor/conf.d/shadowsocks.conf`

```
[program:shadowsocks]
command=sslocal -c /home/b1ng/.shadowsocks.json
autostart=true
autorestart=true
user=b1ng
log_stderr=true
logfile=/var/log/shadowsocks.log
```

编辑文件 `/etc/rc.local`

```
service supervisor start
exit 0
```

### 全局代理
安装 polipo
```
sudo apt-get install polipo
```
修改 polipo 的配置文件 `/etc/polipo/config`
```
logSyslog = true
logFile = /var/log/polipo/polipo.log

proxyAddress = "0.0.0.0"

socksParentProxy = "127.0.0.1:1080"
socksProxyType = socks5

chunkHighMark = 50331648
objectHighMark = 16384

serverMaxSlots = 64
serverSlots = 16
serverSlots1 = 32
```
重启 polipo 服务

```
sudo /etc/init.d/polipo restart
```
polipo默认运行在8123端口，可以通过以下方式测试是否连接成功
```
export http_proxy="http://127.0.0.1:8123/"
curl ip.gs
unset http_proxy
```

## chrome

### Proxy SwitchyOmega
[SwitchyOmega](https://github.com/FelisCatus/SwitchyOmega/releases) 是一个代理设置工具，用于便捷地管理多个代理以及在代理之间切换。


### GFWList

https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList.bak


## 参考
- [Shadowsocks 使用说明](https://github.com/shadowsocks/shadowsocks/wiki/Shadowsocks-%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E)
- [Configuration via Config File](https://github.com/shadowsocks/shadowsocks/wiki/Configuration-via-Config-File)
- [windows 客户端](https://github.com/shadowsocks/shadowsocks-windows/releases)
- [chrome 插件](https://github.com/FelisCatus/SwitchyOmega/releases)
- [GFWList](https://github.com/FelisCatus/SwitchyOmega/wiki/GFWList)
- [linux-ubuntu下安装Shadowsocks服务](https://aitanlu.com/linux-ubuntu-install-shadowsocks.html)
- [ubuntu+shadowsocks+polipo做全局代理](http://dearmadman.com/2015/08/30/use-shadowsocks-in-ubuntu/)
- [为终端设置Shadowsocks代理](http://droidyue.com/blog/2016/04/04/set-shadowsocks-proxy-for-terminal/index.html)
- [Ubuntu server命令行配置shadowsocks全局代理](https://jingsam.github.io/2016/05/08/setup-shadowsocks-http-proxy-on-ubuntu-server.html)
