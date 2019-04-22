# https

传输层安全协议（英语：Transport Layer Security，缩写：TLS）。及其前身安全套接层（Secure Sockets Layer，缩写：SSL）是一种安全协议，目的是为互联网通信，提供安全及数据完整性保障。

## letsencrypt


#### certbot

[certbot](https://certbot.eff.org/#centosrhel7-nginx) 使用 webroot 的方式进行生成，执行命令

```
# 安装 certbot
yum install certbot

# webroot 验证
certbot certonly --webroot -w /usr/share/nginx/html -d domain.com -m email@email.com --agree-tos

# 更新证书
/usr/bin/certbot renew --force-renewal

# crontab 定时任务
crontab -e
0 0 1 */1 * /usr/bin/certbot renew --force-renewal
```

#### acme.sh

安装 [acme.sh](https://acme.sh/)

```
curl  https://get.acme.sh | sh
```

生成证书

```
acme.sh --issue -d mydomain.com --webroot  /usr/share/nginx/html
```

安装证书

```
acme.sh --installcert -d domain.com   \
        --key-file    /etc/nginx/ssl/domain.com \
        --fullchain-file /etc/nginx/ssl/fullchain.cer \
        --reloadcmd  "service nginx force-reload"
```

更新：目前证书在 60 天以后会自动更新

#### Docker
```
docker run -it --rm --name certbot \
           -v "/etc/letsencrypt:/etc/letsencrypt" \
           -v "/var/lib/letsencrypt:/var/lib/letsencrypt" \
           -v "/usr/share/nginx/html:/data/www" \
           certbot/certbot \
           certonly --webroot \
           --webroot-path /data/www \
           --email zhuluojimall@gmail.com \
           -d toutiaopro.com
```

参考

- https://www.humankode.com/ssl/how-to-set-up-free-ssl-certificates-from-lets-encrypt-using-docker-and-nginx
- https://medium.com/bros/enabling-https-with-lets-encrypt-over-docker-9cad06bdb82b
- https://dev.to/domysee/setting-up-a-reverse-proxy-with-nginx-and-docker-compose-29jg

## 参考
[https 配置生成器](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
mozilla https 配置

[crontab.guru](https://crontab.guru/#0_0_1_*/1_*)
crontab 配置图解

[Let's Encrypt 给网站加 HTTPS 完全指南](https://ksmx.me/letsencrypt-ssl-https/)
使用 certbot 给网站 https 的过程，比较详细

[如何免费的让网站启用HTTPS](https://coolshell.cn/articles/18094.html)


## 问题
- openssl 是什么？
- nginx 中的配置项 ssl_trusted_certificate 是什么，怎么配置？


