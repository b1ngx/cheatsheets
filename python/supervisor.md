# supervisor

安装

```
pip install supervisor
```

安装完 supervisor 之后，可以运行echo_supervisord_conf 命令输出默认的配置项，也可以重定向到一个配置文件里：

```
echo_supervisord_conf > /etc/supervisord.conf
```

启动 `supervisord`（通过 -c 选项指定配置文件路径，如果不指定会按照这个顺序查找配置文件：`$CWD/supervisord.conf, $CWD/etc/supervisord.conf, /etc/supervisord.conf）`

```
supervisord -c /etc/supervisord.conf
```

查看 supervisord 是否在运行：

```
ps aux | grep supervisord
```

新建一个目录 `/etc/supervisor` 用于存放这些配置文件，修改 `/etc/supervisord.conf` 里 include 部分的配置：

```
[include]
files = /etc/supervisor/*.conf
```

配置文件格式如下：

```
[program:app]
directory = /home/leon/projects/app ; 程序的启动目录
command = gunicorn -w 8 -b 0.0.0.0:17510 wsgi:app  ; 启动命令
autostart = true     ; 在 supervisord 启动的时候也自动启动
startsecs = 5        ; 启动 5 秒后没有异常退出，就当作已经正常启动了
autorestart = true   ; 程序异常退出后自动重启
startretries = 3     ; 启动失败自动重试次数，默认是 3
user = leon          ; 用哪个用户启动
redirect_stderr = true  ; 把 stderr 重定向到 stdout，默认 false
stdout_logfile_maxbytes = 20MB  ; stdout 日志文件大小，默认 50MB
stdout_logfile_backups = 20     ; stdout 日志文件备份数
; stdout 日志文件，需要注意当指定目录不存在时无法正常启动，所以需要手动创建目录（supervisord 会自动创建日志文件）
stdout_logfile = /data/logs/usercenter_stdout.log
```

其中 [program:app] 中的 app 是应用程序的唯一标识，不能重复。对该程序的所有操作（start, restart 等）都通过名字来实现。

命令

```
supervisorctl reread
supervisorctl update
supervisorctl status
supervisorctl stop app
supervisorctl start app
supervisorctl restart app
```

参考

* [使用 supervisor 管理进程](http://liyangliang.me/posts/2015/06/using-supervisor/)

开机启动

进入目录 /usr/lib/systemd/system/，增加文件 supervisord.service，来使得机器启动的时候启动supervisor，文件内容

```
# supervisord service for systemd (CentOS 7.0+)
# by ET-CS (https://github.com/ET-CS)
[Unit]
Description=Supervisor daemon

[Service]
Type=forking
ExecStart=/usr/bin/supervisord -c /etc/supervisord.conf
ExecStop=/usr/bin/supervisorctl $OPTIONS shutdown
ExecReload=/usr/bin/supervisorctl $OPTIONS reload
KillMode=process
Restart=on-failure
RestartSec=42s

[Install]
WantedBy=multi-user.target
```

systemctl 命令：

```
systemctl enable supervisord
systemctl start supervisord
systemctl stop supervisord
systemctl reload supervisord
```

参考：

- [在centos7上使用systemd启动supervisor](http://www.jianshu.com/p/e1c3e6fbae80)

