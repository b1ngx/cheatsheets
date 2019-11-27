# docker

## Prerequisites

CentOS 7
Linux kernel 3.10.0-693
overlay2

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
- [Get Docker CE for CentOS](https://docs.docker.com/install/linux/docker-ce/centos/#install-docker-ce)

#### 配置
编辑 `/etc/docker/daemon.json` 文件.

```
{
  "exec-opts": ["native.cgroupdriver=systemd"],
  "log-driver": "json-file",
  "log-opts": {
    "max-size": "100m"
  },
  "storage-driver": "overlay2"
}
```
- [Use the OverlayFS storage driver](https://docs.docker.com/storage/storagedriver/overlayfs-driver/)

#### 镜像加速
编辑 `/etc/docker/daemon.json` 文件.

```
{
  "registry-mirrors": [
    "https://registry.docker-cn.com",
    "http://hub-mirror.c.163.com",
    "http://docker.mirrors.ustc.edu.cn",
    "http://dockerhub.azk8s.cn"
  ]
}
```
- [the China registry mirror](https://docs.docker.com/registry/recipes/mirror/#use-case-the-china-registry-mirror)

#### 内核参数

默认配置下，如果在 CentOS 使用 Docker CE 看到下面的这些警告信息：

```
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
```

添加内核配置参数以启用这些功能

```
tee -a /etc/sysctl.conf <<-EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

#重新加载，使配置生效
sysctl -p
```

#### 用户组
```
#建立 docker 组：
groupadd docker

#将当前用户加入 docker 组：
usermod -aG docker $USER

#退出当前终端并重新登录，
```

#### 参考：
- [CentOS 安装 Docker CE](https://yeasy.gitbooks.io/docker_practice/content/install/centos.html)

## 镜像
docker images
docker rmi images_id
docker rmi $(docker images -q)

## 容器
docker run -t -i container_id
docker ps
docker rm container_id
docker rm $(docker ps -aq)

## Dockerfile
FROM
RUN
EXPORE
CMD
WORKDIR
ADD

## compose

## 卸载

```
yum remove docker-ce
rm -rf /var/lib/docker
```




