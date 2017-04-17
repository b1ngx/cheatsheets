## selenium
webdriver.Chrome() 报错 'chromedriver' executable needs to be in PATH.
下载 `chromedriver` ，然后移动到 `/usr/local/bin/chromedriver` 目录下。

## phantomjs
Unable to load Atom 'find_element' from file ':/ghostdriver/./third_party/webdriver-atoms/find_element.js'
not full-function Phantomjs installed by apt-get
1. tar -xvf phantomjs-1.9.7-linux-x86_64.tar.bz2
2. sudo mv phantomjs-1.9.7-linux-x86_64 /usr/local/share/phantomjs
3. sudo ln -sf /usr/local/share/phantomjs/bin/phantomjs /usr/local/bin/phantomjs

## mitmproxy
mitmproxy 是用 Python 和 C 开发的一个中间人代理软件（man-in-the-middle proxy），它可以用来拦截、修改、重放和保存HTTP/HTTPS 请求。

> ?： 查看帮助
C：选择内容到剪切板
E：保存请求到文件

## ref
- [使用 mitmproxy 监控 HTTP 请求](http://liuxiang.logdown.com/posts/192057-use-mitmproxy-to-monitor-http-requests)
- [和Charles同样强大的iOS免费抓包工具mitmproxy](https://mp.weixin.qq.com/s?__biz=MzI5MjEzNzA1MA==&mid=2650264262&idx=1&sn=4e39741c236d7a0c03c5955c4efcf67f)

## XPath
[XPath 教程](http://www.ziqiangxuetang.com/xpath/xpath-intro.html)
