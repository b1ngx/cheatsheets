# https

传输层安全协议（英语：Transport Layer Security，缩写：TLS）。及其前身安全套接层（Secure Sockets Layer，缩写：SSL）是一种安全协议，目的是为互联网通信，提供安全及数据完整性保障。

## letsencrypt


#### certbot

[certbot](https://certbot.eff.org/#centosrhel7-nginx) 使用 webroot 的方式进行生成，执行命令

```
# 安装
yum install certbot

# obtain

certbot --nginx

# renewal
/usr/bin/certbot renew --dry-run

# 定时更新
crontab -e
0 0,12 * * * . /etc/profile; python -c 'import random; import time; time.sleep(random.random() * 3600)' && certbot renew
```

#### Docker

docker-compose.yml

```
nginx:
    image: nginx
    ports:
      - 80:80
      - 443:443
    volumes:
      - /var/log/nginx:/var/log/nginx
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
      - /etc/letsencrypt:/etc/letsencrypt
      - /var/www/letsencrypt:/var/www/letsencrypt
    restart: always
```

nginx.conf

```
location ~ /.well-known/acme-challenge {
            allow all;
            root /var/www/letsencrypt;
        }
```

生成证书

```
docker run -it --rm --name certbot \
           -v "/etc/letsencrypt:/etc/letsencrypt" \
           -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
           -v "/var/www/letsencrypt:/var/www/letsencrypt" \
           certbot/certbot \
           certonly --webroot \
           --webroot-path /var/www/letsencrypt \
           --email example@gmail.com \
           -d example.com
```

更新证书

```
docker run -it --rm --name certbot \
           -v "/etc/letsencrypt:/etc/letsencrypt" \
           -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
           -v "/var/www/letsencrypt:/var/www/letsencrypt" \
           certbot/certbot \
           renew
```

重启 nginx, that's ok.

参考

- https://www.humankode.com/ssl/how-to-set-up-free-ssl-certificates-from-lets-encrypt-using-docker-and-nginx
- https://medium.com/bros/enabling-https-with-lets-encrypt-over-docker-9cad06bdb82b
- https://dev.to/domysee/setting-up-a-reverse-proxy-with-nginx-and-docker-compose-29jg

#### ubuntu
解决设置 `sudo add-apt-repository ppa:certbot/certbot` 或更新 `apt update` paa 时的网络问题


1. 查找 certbot 的 ppa 源，https://launchpad.net/~certbot/+archive/ubuntu/certbot
2. 修改为 科大 LUG 的源，https://lug.ustc.edu.cn/wiki/mirrors/help/revproxy
3. ⚠️注意需要为 **https**

修改 `/etc/apt/source.list` 

```
deb https://launchpad.proxy.ustclug.org/certbot/certbot/ubuntu bionic main
```

参考：https://github.com/ustclug/mirrorrequest/issues/43

## 参考

Mozilla SSL Configuration Generator
[https://ssl-config.mozilla.org/](https://ssl-config.mozilla.org/)

crontab 配置图解
[crontab.guru](https://crontab.guru/#0_0_1_*/1_*)

[Let's Encrypt 给网站加 HTTPS 完全指南](https://ksmx.me/letsencrypt-ssl-https/)
使用 certbot 给网站 https 的过程，比较详细

[如何免费的让网站启用HTTPS](https://coolshell.cn/articles/18094.html)


## 问题
- openssl 是什么？
- nginx 中的配置项 ssl_trusted_certificate 是什么，怎么配置？


