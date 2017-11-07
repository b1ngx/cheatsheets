# nginx

## 命令

```
systemctl start nginx     //启动服务
systemctl stop nginx      //停止服务
systemctl enable nginx    //开机启动服务
systemctl restart nginx   //重新加载配置

//301 重定向
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

- [How To Install Nginx on CentOS 7](https://www.digitalocean.com/community/tutorials/how-to-install-nginx-on-centos-7)
centos 7 nginx 安装指南

- [Nginx基本配置备忘](https://zhuanlan.zhihu.com/p/24524057)
nginx 配置 & https


