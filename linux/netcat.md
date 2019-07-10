# nc
arbitrary TCP and UDP connections and listens

## 安装

```
yum install nc
```

## Usage

#### 目录传输

1.在本机上执行命令

```
tar -c app | nc -l 9999
```

2.在接收文件的机器上执行命令

```
nc 192.168.1.243 9999 | tar -x
```


在A机器上有app目录，需要传输到B机  A机器IP：192.168.1.243

A机器： 

```
tar -cf - ./app | nc -l 1234
``` 

B机器：

```
nc 192.168.1.243 1234 | tar -xf -
```

#### 端口扫描

```
nc -z -v -n 192.168.1.243 21-25
```

`-z` 连接成功后立即关闭，不传输数据
`-v` 详细输出
`-n` 不要使用DNS反向查询IP地址的域名

## 参考
[Linux Netcat 命令——网络工具中的瑞士军刀](http://www.oschina.net/translate/linux-netcat-command)


