# java

## Step
1. 检查是否安装旧版本 ` java -version ` ，卸载旧版本
2. 访问 [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 下载最新 jdk 版本
3. 安装 `rpm -ivh jdk-8u151-linux-x64.rpm`

## Usage

1、安装 `openjdk`

```
yum install java-1.8.0-openjdk
```

2、安装 `orcle jdk`

``` 
# 下载
wget --no-cookies --no-check-certificate --header "Cookie: oraclelicense=accept-securebackup-cookie" "http://download.oracle.com/otn-pub/java/jdk/8u161-b12/2f38c3b165be4555a1fa6e98c45e0808/jdk-8u161-linux-x64.rpm" 

# 安装
rpm -ivh jdk-8u161-linux-x64.rpm
```

检查是否安装成功

```
[root@localhost ~]# java -version
java version "1.8.0_151"
Java(TM) SE Runtime Environment (build 1.8.0_151-b12)
Java HotSpot(TM) 64-Bit Server VM (build 25.151-b12, mixed mode)
```

环境变量设置

```
export JAVA_HOME=/usr/java/latest
export PATH=$PATH:$JAVA_HOME
```

卸载

```
rpm -qa | grep jdk
yum -y remove jdk1.8-1.8.0_151-fcs.x86_64 
```

## ref
http://openjdk.java.net/install/


