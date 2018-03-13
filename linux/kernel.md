# kernel 升级

升级 linux kernel，[Centos 7 kernel elrepo](http://elrepo.org/linux/kernel/el7/x86_64/RPMS/)

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

内核升级完成后，新老内核会同时存在，CentOS 7 使用 grub2 引导程序，需要将最新内核优先级调整最高。

```
#设置启动顺序
grub2-set-default 0

#重启
reboot

#查看内核版本
uname -r
```

删除旧内核

```
#查看已安装的内核
rpm -qa | grep kernel

#删除没有使用的内核
yum -y remove kernel kernel-tools
```

## 参考
- [升级Centos 7/6内核版本到4.12.4的方法](https://www.centos.bz/2017/08/upgrade-centos-7-6-kernel-to-4-12-4/)
- [CentOS 6/7升级最新内核并开启Google BBR](https://www.centos.bz/2018/01/centos-6-7%E5%8D%87%E7%BA%A7%E6%9C%80%E6%96%B0%E5%86%85%E6%A0%B8%E5%B9%B6%E5%BC%80%E5%90%AFgoogle-bbr/)

