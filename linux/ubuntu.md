# ubuntu

## Install

#### UNetbootin

- [UNetbootin](https://unetbootin.github.io/)

#### dd
[如何通过 USB 设备来安装 CentOS](https://wiki.centos.org/zh/HowTos/InstallFromUSBkey)

```
diskutil list
diskutil unmountDisk /dev/disk1
dd if=CentOS-6.5-x86_64-bin-DVD1.iso of=/dev/sdb
```

##### Ubuntu 16.04 找不到硬盘
需将硬盘模式改为 IDE，否则出现找不到硬盘，16.10 版本支持 ACHI.

## Setup
18.04 LTS

#### mirror
https://mirror.tuna.tsinghua.edu.cn/help/ubuntu/

#### DNS
修改文件 `/etc/network/interfaces` 添加 `dns-nameservers 8.8.8.8`
或 `/etc/resolvconf/resolv.conf.d/base` 添加 `nameserver 8.8.8.8`
通过命令 `cat /etc/resolv.conf` 查看效果

#### docker
https://docs.docker.com/install/linux/docker-ce/ubuntu/

#### nginx
http://nginx.org/en/linux_packages.html#Ubuntu

#### certbot
https://certbot.eff.org/


