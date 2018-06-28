# Kolla

## Centos

最小化安装 centos 后，进行初始化设置

#### 关闭Selinux

关闭 selinux，编辑 `/etc/selinux/config`

```
SELINUX=disabled
```

重启机器，查看状态

```
sestatus
SELinux status:                 disabled
```

#### 关闭Firewall

```
systemctl status firewalld
systemctl stop firewalld
systemctl disable firewalld
firewall-cmd --state
```

#### 修改Hostname

修改 hostname

```
vim /etc/hostname
kolla
```

修改 hosts

```
vim /etc/hosts
```

检查

```
hostname
kolla

hostname -f
```

#### 安装依赖
```
yum install epel-release
yum install python-pip
pip install -U pip

yum install python-devel libffi-devel gcc openssl-devel libselinux-python
```

## docker

1、安装

```
# Install required packages. 
yum install -y yum-utils device-mapper-persistent-data lvm2

# set up the stable repository
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

yum install docker-ce
```

2、设置

```
mkdir /etc/systemd/system/docker.service.d

vim kolla.conf
[Service]
MountFlags=shared
```

3、服务

```
systemctl daemon-reload
systemctl enable docker
systemctl restart docker
```

## kolla

#### ansible

```
yum install ansible
```

#### kolla-ansible

安装

```
yum install kolla-ansible
``` 

复制配置文件

```
cp -r /usr/share/kolla-ansible/etc_examples/kolla /etc/kolla/
cp /usr/share/kolla-ansible/ansible/inventory/* .
```

## 安装
1、生成密码

```
kolla-genpwd
```

2、编辑 `/etc/kolla/globals.yml`

```
kolla_internal_vip_address: "192.168.1.244"
kolla_install_type: "source"
openstack_release: "pike"
network_interface: "enp1s0"
neutron_external_interface: "enp1s0"
```
kolla_internal_vip_address：是一个没有使用的的 ip 地址，给 haproxy 使用。

3、安装 openstack

```
kolla-ansible deploy -i ./all-in-one
```

## 参考
- [kolla-ansible](https://docs.openstack.org/kolla-ansible/latest/user/quickstart.html)
- [OpenStack容器化之路：Kolla项目介绍](http://www.99cloud.net/html/2016/jiuzhouyuanchuang_0625/181.html)
- [容器与OpenStack从相杀到相爱](http://xcodest.me/containerize-openstack.html)
- [Kolla安装Ocata 单节点](http://www.chenshake.com/kolla-installation/)
- [Kolla单节点部署手册](http://blog.csdn.net/moolight_shadow/article/details/52971637)
- [kolla-ansible快速入门](http://www.cnblogs.com/zhangyufei/p/7645804.html)

