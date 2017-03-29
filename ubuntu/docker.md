# docker

## 安装

使用如下命令
```
$ curl -fsSL https://get.docker.com/ | sh
```
参考：https://docs.docker.com/engine/getstarted/linux_install_help/

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

## uninstall
```
sudo apt-get purge docker-engine
sudo apt-get autoremove --purge docker-engine
rm -rf /var/lib/docker
```
https://docs.docker.com/engine/installation/linux/ubuntulinux/#/uninstallation

## nodejs
- https://www.oschina.net/translate/develop-a-nodejs-app-with-docker
- http://www.widuu.com/docker/node.html
