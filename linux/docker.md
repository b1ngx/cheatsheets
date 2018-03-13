# docker

## Prerequisites

升级 linux 内核，官方 Centos 7：http://elrepo.org/linux/kernel/el7/x86_64/RPMS/

```
#导入ELRepo 公钥
rpm -import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
#安装ELRepo
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-3.el7.elrepo.noarch.rpm
#升级最新内核
yum --enablerepo=elrepo-kernel install kernel-ml -y
```

查看内核启动顺序

```
awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg
egrep ^menuentry /etc/grub2.cfg | cut -f 2 -d \'
```

内核升级完成后老的内核和新的会同时存在，CentOS 7 使用 grub2 引导程序，需要将最新内核优先级调整最高。

```
grub2-set-default 0
reboot

#查看内核版本
uname -r
```

## 安装

使用如下命令

```
# Install required packages. 
yum install -y yum-utils

# set up the stable repository
yum-config-manager \
    --add-repo \
    https://mirrors.ustc.edu.cn/docker-ce/linux/centos/docker-ce.repo

yum makecache fast
yum install docker-ce
```

参考：[Get Docker CE for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/#install-docker-ce)

## 镜像
docker images
docker rmi images_id

## 容器
docker run -t -i container_id
docker ps
docker rm container_id

## Dockerfile
FROM
RUN
EXPORE
CMD
WORKDIR
ADD

## 卸载

```
yum remove docker-ce
rm -rf /var/lib/docker
```

## 参考
- [CentOS 安装 Docker CE](https://yeasy.gitbooks.io/docker_practice/content/install/centos.html)
- [升级Centos 7/6内核版本到4.12.4的方法](https://www.centos.bz/2017/08/upgrade-centos-7-6-kernel-to-4-12-4/)
- [CentOS 6/7升级最新内核并开启Google BBR](https://www.centos.bz/2018/01/centos-6-7%E5%8D%87%E7%BA%A7%E6%9C%80%E6%96%B0%E5%86%85%E6%A0%B8%E5%B9%B6%E5%BC%80%E5%90%AFgoogle-bbr/)


