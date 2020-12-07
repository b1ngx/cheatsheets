## Proxy

```bash
export hostip=$(cat /etc/resolv.conf | grep nameserver | awk '{ print $2 }')
export https_proxy="http://${hostip}:7890"
export http_proxy="http://${hostip}:7890"
```

[为 WSL2 一键设置代理](https://zhuanlan.zhihu.com/p/153124468)
[WSL2 Proxy Setting](https://isshiki.medium.com/wsl2-proxy-setting-2647a556c5ec)
