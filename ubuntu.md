- ubuntu U盘装机
[Universal-USB-Installer](http://www.pendrivelinux.com/universal-usb-installer-easy-as-1-2-3/)

- [Ubuntu 16.04 安装基础入门教程（图文）](http://forum.ubuntu.org.cn/viewtopic.php?f=77&t=478527)

- [Ubuntu 安装基础教程](http://teliute.org/linux/Ubsetup/)

- [Ubuntu 16.04 U盘安装图文教程](http://www.linuxidc.com/Linux/2016-04/130520.htm)

- [UNetbootin](https://unetbootin.github.io/)

### 问题
- 安装 Ubuntu 16.04 时需将硬盘模式改为 IDE，否则出现找不到硬盘。
 16.10 版本支持 ACHI.

- 设置 pip 镜像源
创建 ~/.pip/pip.conf 文件
添加设置
```
[global]
index-url = http://pypi.douban.com/simple
[install]
trusted-host = pypi.douban.com
```
http://www.jianshu.com/p/d109e5009c65
http://ryerh.com/python/2016/04/08/installing-scrapy-in-ubuntu.html

 windows 下修改 `%PYTHON_HOME%\Lib\site-packages\pip\cmdoptions.py` 文件

- DNS
修改文件 `/etc/network/interfaces` 添加 `dns-nameservers 8.8.8.8`
或 `/etc/resolvconf/resolv.conf.d/base` 添加 `nameserver 8.8.8.8`
通过命令 `cat /etc/resolv.conf` 查看效果
