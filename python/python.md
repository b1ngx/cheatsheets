# awesome

- [Python 教程](http://goo.gl/M3yI71)
  廖雪峰的 python 教程
  
- [Python Cookbook 3rd Edition](Python Cookbook 3rd Edition Documentation)
- [Python 3 Module of the Week](https://pymotw.com/3/index.html)

## windows 平台出现的错误


### 安装 scrapy 出现 `error: Unable to find vcvarsall.bat`

[How to deal with the pain of “unable to find vcvarsall.bat”](https://blogs.msdn.microsoft.com/pythonengineering/2016/04/11/unable-to-find-vcvarsall-bat/) 
windows 上安装 python 最好先安装 vs

### Could not find function xmlCheckVersion in library libxml2. Is libxml2 installed?

解决办法：http://www.lfd.uci.edu/~gohlke/pythonlibs/#lxml 下载 `lxml-3.6.1-cp35-cp35m-win32.whl`
解压，后 copy 到 `C:\Users\BinG\AppData\Local\Programs\Python\Python35-32\Lib\site-packages` 目录

### ImportError: cannot import name '_win32stdio'
Unfortunately twisted.internet._win32stdio is not ported to Python 3 yet: it means Scrapy doesn't support Python 3 on Windows at the moment.

参考：https://github.com/scrapy/scrapy/issues/1998
https://github.com/crossbario/crossbar/issues/557
http://stackoverflow.com/questions/37342603/importerror-cannot-import-name-win32stdio

