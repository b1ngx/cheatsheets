# vim

## 安装

手动安装
```
sudo apt install git
git clone https://github.com/vim/vim.git
cd vim
./configure
sudo apt install ncurses-dev
make
sudo make install
```

## 剪贴板
### 简单复制和粘贴
vim提供12个剪贴板，它们的名字分别为vim有11个粘贴板，分别是`0`、`1`、`2`、`...`、`9`、`a`、`“`。如果开启了系统剪贴板，则会另外多出两个：`+`和`*`。使用`:reg`命令，可以查看各个粘贴板里的内容。

  在vim中简单用y只是复制到`“`（双引号)粘贴板里，同样用p粘贴的也是这个粘贴板里的内容。

### 复制和粘贴到指定剪贴板
要将vim的内容复制到某个粘贴板，需要退出编辑模式，进入正常模式后，选择要复制的内容，然后按"Ny完成复制，其中N为粘贴板号（注意是按一下双引号然后按粘贴板号最后按y），例如要把内容复制到粘贴板a，选中内容后按"ay就可以了。

  要将vim某个粘贴板里的内容粘贴进来，需要退出编辑模式，在正常模式按"Np，其中N为粘贴板号。比如，可以按"5p将5号粘贴板里的内容粘贴进来，也可以按"+p将系统全局粘贴板里的内容粘贴进来。

### 系统剪贴板

  Vim支持系统剪贴板，需要打开clipboard功能。使用下面的命令，检查当前版本的Vim，是否支持clipboard。

  ```bash
  $ vim --version
  ```

  如果不支持的话，需要安装图形化界面的vim（即gvim），或者重新编译vim。

  ```bash
  $ sudo apt-get install gvim
  正在读取软件包列表... 完成
  正在分析软件包的依赖关系树
  正在读取状态信息... 完成
  Package gvim is a virtual package provided by:
    vim-gtk 2:7.4.488-7
    vim-gnome 2:7.4.488-7
    vim-athena 2:7.4.488-7
  You should explicitly select one to install.

  E: Package 'gvim' has no installation candidate

  $ sudo apt-get install vim-gnome
  ```

  另一种方法，是安装vim-gui-common。

  ```bash
  $ sudo apt-get install vim-gui-common
  ```

  安装以后，可以用命令行界面，启动gvim，这时可用系统剪贴板。

  ```bash
  $ gvim -v
  ```

  星号（`*`）和加号（`+`）粘贴板是系统粘贴板。在windows系统下， * 和 + 剪贴板是相同的。对于 X11 系统， * 剪贴板存放选中或者高亮的内容， + 剪贴板存放复制或剪贴的内容。打开clipboard选项，可以访问 + 剪贴板；打开xterm_clipboard，可以访问 * 剪贴板。 * 剪贴板的一个作用是，在vim的一个窗口选中的内容，可以在vim的另一个窗口取出。

  复制到系统剪贴板
  - `"*y`
  - `"+y`
  - `"+2yy` – 复制两行
  - `{Visual}"+y` - copy the selected text into the system clipboard
  - `"+y{motion}` - copy the text specified by {motion} into the system clipboard
  - `:[range]yank +` - copy the text specified by `[range]` into the system clipboard

  剪切到系统剪贴板
  - `"+dd` – 剪切一行

  从系统剪贴板粘贴到vim
  - `"*p`
  - `"+p`
  - `Shift+Insert`
  - `:put +` - Ex command puts contents of system clipboard on a new line
  - `<C-r>`+ - From insert mode (or commandline mode)

  `"+p`比 Ctrl-v 命令更好，它可以更快更可靠地处理大块文本的粘贴，也能够避免粘贴大量文本时，发生每行行首的自动缩进累积，因为`Ctrl-v`是通过系统缓存的stream处理，一行一行地处理粘贴的文本。

## 让 vim 支持 clipboard
ubuntu中系统默认的vim真是折腾,竟然不支持 `+clipboard`.

如果没有开启clipboard特性,那vim就没法和系统的粘贴板交互,也就是说我们用 `"+y` 命令复制之后,没办法粘贴到其他地方,比如浏览器等.

`vim-gnome` 这个包给vim提供了 `+clipboard` 特性.我们只需要安装一下就可以了.
```
sudo apt-get install vim-gnome
```
然后再查看一下,应该已经成功开启了:
```
vim --version | grep clipboard
```
## ref
- https://github.com/ruanyf/articles/blob/master/dev/vim/operation.md
- http://hushicai.com/2016/01/08/rang-vim-zhi-chi-clipboard.html
- http://codingpy.com/article/vim-and-python-match-in-heaven/
