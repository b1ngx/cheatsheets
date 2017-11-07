# nodejs

## 安装

```
curl -sL https://deb.nodesource.com/setup_7.x | sudo -E bash -
sudo apt-get install -y nodejs
```

https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions

## nvm
https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-a-centos-7-server
四种安装方式，最靠谱的是 [nvm](https://github.com/creationix/nvm)，强烈推荐

## pm2
Advanced, production process manager for Node.js

centos 下指定[端口](https://github.com/Unitech/pm2/issues/428#issuecomment-176726334)号

> In order to start an app on port 3000 you could say `PORT=3000 pm2 start app.js` in Terminal.

```
PORT=2016 pm2 start ./bin/www
```

## npm
设置淘宝镜像源

```
npm config set registry https://registry.npm.taobao.org
```

## 参考链接
- [nvm](https://github.com/creationix/nvm)
- [pm2](https://github.com/Unitech/pm2)
- [How To Set Up a Node.js Application for Production on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-node-js-application-for-production-on-centos-7)
- https://github.com/Unitech/pm2/issues/428#issuecomment-176726334


