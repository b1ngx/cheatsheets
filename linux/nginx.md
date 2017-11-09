# nginx

## 安装

To add NGINX yum repository, create a file named /etc/yum.repos.d/nginx.repo and paste one of the configurations below:

```
[nginx]
name=nginx repo
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/
gpgcheck=0
enabled=1
```

## 命令

```
systemctl start nginx     //启动服务
systemctl enable nginx    //开机启动服务
systemctl restart nginx   //重新加载配置
```

## configure

301 重定向

```
server {
    server_name abc.com;
    rewrite ^/(.*)$ http://www.abc.com/$1 permanent;
}
```

## 参考
- [官方指南](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-red-hat-centos-packages)
nginx 官方文档

- [Nginx HTTP server boilerplate configs](https://github.com/h5bp/server-configs-nginx)
nginx 参考配置模板

- [Nginx基本配置备忘](https://zhuanlan.zhihu.com/p/24524057)
nginx 配置 & https

- [Centos下 Nginx安装与配置](http://www.jianshu.com/p/d5114a2a2052)
  手动（manual）安装 nginx

