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

```
cat>/etc/apt/sources.list<<EOF
# 默认注释了源码镜像以提高 apt update 速度，如有需要可自行取消注释
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
EOF
```

#### DNS
修改 `/etc/netplan/01-netcfg.yaml`

```
network:
    version: 2
    renderer: NetworkManager
    ethernets:
        eth0:
            dhcp4: true
            nameservers:
                addresses: [1.1.1.1,1.0.0.1]
```

Once done save the file and apply the changes with

```
$ sudo netplan --debug apply
```

To verify that the new DNS resolvers are set, run the following command

```
$ systemd-resolve --status | grep 'DNS Servers' -A2
```

https://linuxize.com/post/how-to-set-dns-nameservers-on-ubuntu-18-04/

#### docker
https://docs.docker.com/install/linux/docker-ce/ubuntu/

#### nginx
http://nginx.org/en/linux_packages.html#Ubuntu

#### certbot
https://certbot.eff.org/


