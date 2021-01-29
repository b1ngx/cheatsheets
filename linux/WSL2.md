Windows Setup

## Windows

#### 安装

以下介绍的是如何尽可能仅用微软的资源制作 Windows 10 安装 U 盘。

1、访问 www.microsoft.com/zh-cn/software-download/windows10 可以得到微软提供的全自动制作 Windows 10 安装介质的工具“MediaCreationTool” 。

2、如果将浏览器的 User Agent 修改为某个移动浏览器，再去访问 www.microsoft.com/zh-cn/software-download/windows10 就会被定向到一个可以下载 Windows 10 的 ISO 的页面。

下载后可用 Windows 自带的命令行工具 `Get-FileHash` 校验文件 HASH：

```
Get-FileHash Win10_1903_V1_Chinese(Simplified)_x64.iso
```

3、微软曾为 Windows 7 提供了一个 Windows USB/DVD Download Tool www.microsoft.com/en-us/download/details.aspx?id=56485，可从 ISO 文件制作自启动 U 盘安装介质。这个工具也适用于 Windows 10。

参考：https://weibo.com/1401527553/I2kwriOS6?type=comment

#### 激活

激活命令

```bash
slmgr /ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
slmgr /skms kms.03k.org
slmgr /ato
```

参考：[Windows 10 最新版激活方式，免费升级到20H2](https://www.freedidi.com/1038.html)



## Office

#### 自定义安装



## WSL2

### 安装

[Windows Subsystem for Linux Installation Guide for Windows 10]([Install Windows Subsystem for Linux (WSL) on Windows 10 | Microsoft Docs]([在 Windows 10 上安装适用于 Linux 的 Windows 子系统 (WSL) | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/wsl/install-win10))



### 从 Windows (localhost) 访问 Linux 网络应用

如果要在 Linux 分发版中构建网络应用（例如，在 NodeJS 或 Python 上运行的应用），可以使用 `localhost` 从 Windows 应用（如 Microsoft Edge 或 Chrome 浏览器）访问它（就像往常一样）。

若要查找为 Linux 分发版提供支持的虚拟机的 IP 地址，请执行以下操作：

- 在 WSL 分发版（即 Ubuntu）中运行以下命令：`ip addr`
- 查找并复制 `eth0` 接口的 `inet` 值下的地址。
- 如果已安装 grep 工具，请通过使用以下命令筛选输出来更轻松地查找此地址：`ip addr | grep eth0`
- 使用此 IP 地址连接到 Linux 服务器。



### 从 Linux（主机 IP）访问 Windows 网络应用

如果要从 Linux 分发版（即 Ubuntu）访问 Windows 上运行的网络应用（例如，在 NodeJS 或 SQL 服务器上运行的应用），则需要使用主机的 IP 地址。 虽然这不是一种常见方案，但你可以执行以下步骤来使其可行。

1. 通过在 Linux 分发版中运行以下命令来获取主机的 IP 地址：`cat /etc/resolv.conf`
2. 复制以下词语后面的 IP 地址：`nameserver`。
3. 使用复制的 IP 地址连接到任何 Windows 服务器。

设置代理

```
export hostip=$(cat /etc/resolv.conf | grep nameserver | awk '{ print $2 }')
export https_proxy="http://${hostip}:7890"
export http_proxy="http://${hostip}:7890"
```



#### 从局域网 (LAN) 访问 WSL 2 分发版

当使用 WSL 1 分发版时，如果计算机设置为可供 LAN 访问，那么在 WSL 中运行的应用程序也可供在 LAN 中访问。

这不是 WSL 2 中的默认情况。 WSL 2 有一个带有其自己独一无二的 IP 地址的虚拟化以太网适配器。 目前，若要启用此工作流，你需要执行与常规虚拟机相同的步骤。 （我们正在寻找改善此体验的方法。）

下面是一个示例 PowerShell 命令，用于添加侦听主机上的端口 4000 的端口代理并将其连接到端口 4000，并使用 IP 地址 192.168.101.100 连接到 WSL 2 VM。

```
netsh interface portproxy add v4tov4 listenport=4000 listenaddress=0.0.0.0 connectport=4000 connectaddress=192.168.101.100
```

与 netsh 相关的命令：

```
netsh interface portproxy show v4tov4
netsh interface portproxy reset
```



### 参考

- [从 Linux（主机 IP）访问 Windows 网络应用](https://docs.microsoft.com/zh-cn/windows/wsl/compare-versions#accessing-windows-networking-apps-from-linux-host-ip)

- [为 WSL2 一键设置代理](https://zhuanlan.zhihu.com/p/153124468)
- [WSL2 Proxy Setting](https://isshiki.medium.com/wsl2-proxy-setting-2647a556c5ec)

