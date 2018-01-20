# how to install install python on centos7 

## 系统环境
centos 7.4
python 3.6.4

## 准备
```
yum update
# Compilers and related tools:
yum groupinstall -y "development tools"
# Libraries needed during compilation to enable all features of Python:
yum install -y zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel expat-devel
# If you are on a clean "minimal" install of CentOS you also need the wget tool:
yum install -y wget
```

## python3
```
# Python 3.6.4:
wget https://www.python.org/ftp/python/3.6.4/Python-3.6.4.tar.xz
tar xzf Python-3.6.4.tar.xz
cd Python-3.6.4
./configure --prefix=/usr/local --enable-shared LDFLAGS="-Wl,-rpath /usr/local/lib"
make && make altinstall
```

## 参考
- [How to Install Python 2.7.14 on CentOS](https://danieleriksson.net/2017/02/08/how-to-install-latest-python-on-centos/)
- [How to install the latest version of Python on CentOS](https://tecadmin.net/install-python-2-7-on-centos-rhel/)


