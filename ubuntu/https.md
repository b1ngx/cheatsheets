# https

传输层安全协议（英语：Transport Layer Security，缩写：TLS）。及其前身安全套接层（Secure Sockets Layer，缩写：SSL）是一种安全协议，目的是为互联网通信，提供安全及数据完整性保障。

## openssl
是什么？

## SSL 证书机构
https://letsencrypt.org/  过期时间 90 天

https://www.startssl.com/ 免费的 Class 1 SSL 证书支持 5 个域名

## https
[https 配置生成器](https://mozilla.github.io/server-side-tls/ssl-config-generator/)

## letsencrypt
[Let's Encrypt 给网站加 HTTPS 完全指南](https://ksmx.me/letsencrypt-ssl-https/)
使用 certbot 给网站 https 的过程，比较详细

[Certbot](https://certbot.eff.org/#centosrhel7-nginx)
使用 webroot 的方式进行生成

执行命令
` certbot certonly --webroot -w /usr/share/nginx/html/ -d www.yunliewang.com -d yunliewang.com`

## 衍生品
[gethttpsforfree](https://gethttpsforfree.com)
[sslforfree](https://www.sslforfree.com/)
[acme.sh](https://acme.sh/)

## 参考
[数字签名是什么？](http://www.ruanyifeng.com/blog/2011/08/what_is_a_digital_signature.html)
[Mozilla 宣布计划逐步淘汰 HTTP](http://idarkside.org/posts/mozilla-deprecating-non-secure-http)

[nginx配置ssl加密](http://seanlook.com/2015/05/28/nginx-ssl/)
讲解了只对部分页面加密的示例

[Nginx 配置 SSL 证书 + 搭建 HTTPS 网站教程](https://s.how/nginx-ssl/)
全站https示例

## 问题
nginx 中的配置项 ssl_trusted_certificate 是什么，怎么配置

## 参考
[Let's Encrypt SSL证书配置](http://www.jianshu.com/p/eaac0d082ba2)
