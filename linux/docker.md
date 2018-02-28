# docker

## 安装

使用如下命令

```
# Install required packages. 
yum install -y yum-utils device-mapper-persistent-data lvm2

# set up the stable repository
yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

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


