# nginx

## 安装

###  发行版

查看 http://nginx.org/en/linux_packages.html 选择对应的 linux 发行版进行安装

### 源码安装

> 由于发行版缺少一些必要的模块，或者所以用的版本不符合要去，可以选择从源码安装，选择自己需要的模块。例如 TLS 1.3 需要 openssl 1.1.1 以上。

#### OpenSSL
openssl 从 `1.1.1` 开始支持 `TLSv1.3`

```
wget https://www.openssl.org/source/openssl-1.1.1d.tar.gz
tar zxvf openssl-1.1.1d.tar.gz
mv openssl-1.1.1d openssl
cd openssl
./config
make
make install
```

#### Nginx

```
wget http://nginx.org/download/nginx-1.17.5.tar.gz
tar zxvf nginx-1.17.5.tar.gz
cd nginx-1.17.5

./configure --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib64/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-mail --with-mail_ssl_module --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module --with-cc-opt='-O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions -fstack-protector-strong --param=ssp-buffer-size=4 -grecord-gcc-switches -m64 -mtune=generic -fPIC' --with-ld-opt='-Wl,-z,relro -Wl,-z,now -pie' --with-openssl=../openssl --with-openssl-opt='enable-tls1_3'

make && make install
```

编译参数：http://nginx.org/en/docs/configure.html

### 命令
nginx -v：查看 nginx 版本
nginx -V：查看编译信息
nginx -t：验证配置文件 `/etc/nginx/nginx.conf`



## Service

编辑 `/etc/systemd/system/nginx.service`

```
[Unit]
Description=A high performance web server and a reverse proxy server
After=network.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t -q -g 'daemon on; master_process on;'
ExecStart=/usr/sbin/nginx -g 'daemon on; master_process on;'
ExecReload=/usr/sbin/nginx -g 'daemon on; master_process on;' -s reload
ExecStop=-/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid
TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

系统命令：

```
systemctl enable nginx    //开机启动服务
systemctl start nginx     //启动服务
systemctl restart nginx   //重新加载配置
systemctl status nginx    //运行状态
systemctl is-enabled nginx
ps -ef | grep nginx
```

## nginx.conf

```
# For more information on configuration, see:
#   * Official English Documentation: http://nginx.org/en/docs/
#   * Official Russian Documentation: http://nginx.org/ru/docs/

user nginx;
worker_processes auto;
error_log /var/log/nginx/error.log info;
pid /run/nginx.pid;

# Load dynamic modules. See /usr/share/nginx/README.dynamic.
include /usr/share/nginx/modules/*.conf;

events {
    worker_connections 1024;
}

http {

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile            on;
    tcp_nopush          on;
    tcp_nodelay         on;
    keepalive_timeout   65;
    types_hash_max_size 2048;

    gzip on;
    gzip_min_length 1k;
    gzip_comp_level 2;
    gzip_proxied expired no-cache no-store private auth;
    gzip_types text/plain text/css text/javascript application/javascript application/x-javascript application/json image/jpeg image/gif image/png;
    gzip_vary on;
    gzip_disable "MSIE [1-6]\.";

    include             /etc/nginx/mime.types;
    default_type        application/octet-stream;

    # Load modular configuration files from the /etc/nginx/conf.d directory.
    # See http://nginx.org/en/docs/ngx_core_module.html#include
    # for more information.
    include /etc/nginx/conf.d/*.conf;

    server {
        listen 80 default_server;
        listen [::]:80 default_server;

        # Redirect all HTTP requests to HTTPS with a 301 Moved Permanently response.
        return 301 https://$host$request_uri;
    }

    server {
        listen 443 ssl http2;
        listen [::]:443 ssl http2;

        # certs sent to the client in SERVER HELLO are concatenated in ssl_certificate
        ssl_certificate /etc/letsencrypt/live/toutiao.keji01.com/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/toutiao.keji01.com/privkey.pem;
        ssl_session_timeout 1d;
        ssl_session_cache shared:SSL:50m;
        ssl_session_tickets off;

        # Diffie-Hellman parameter for DHE ciphersuites, recommended 2048 bits
        ssl_dhparam /etc/nginx/ssl/dhparam.pem;

        # intermediate configuration
        ssl_protocols TLSv1.2 TLSv1.3;
        ssl_ciphers ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384;
        ssl_prefer_server_ciphers off;
    
        # HSTS (ngx_http_headers_module is required) (63072000 seconds)
        add_header Strict-Transport-Security "max-age=63072000" always;
    
        # OCSP stapling
        ssl_stapling on;
        ssl_stapling_verify on;

        location / {
            proxy_pass http://127.0.0.1:8000;
            proxy_set_header Host $host;
            proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        }

        location /static {
            alias /home/gov/collected_static;
        }

        error_page 404 /404.html;
            location = /40x.html {
        }

        error_page 500 502 503 504 /50x.html;
            location = /50x.html {
        }

    }

}
```

## Docker

在 docker 中做反向代理的时候，docker 网络的问题

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    location / {
        proxy_pass http://webapp;
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    }
}

upstream webapp {
    server webapp:5042;
}
```

参考：

- https://medium.com/@joatmon08/using-containers-to-learn-nginx-reverse-proxy-6be8ac75a757
- https://www.thepolyglotdeveloper.com/2017/03/nginx-reverse-proxy-containerized-docker-applications/

## ref
- [官方指南](https://www.nginx.com/resources/wiki/start/topics/tutorials/install/#official-red-hat-centos-packages)
nginx 官方文档

- [Nginx HTTP server boilerplate configs](https://github.com/h5bp/server-configs-nginx)
nginx 参考配置模板

- [Nginx基本配置备忘](https://zhuanlan.zhihu.com/p/24524057)
nginx 配置 & https

- [Centos下 Nginx安装与配置](http://www.jianshu.com/p/d5114a2a2052)
  手动（manual）安装 nginx
  
- https://imququ.com/post/enable-tls-1-3.html

