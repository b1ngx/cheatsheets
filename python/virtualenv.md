# virtualenv

## 安装
```
sudo pip install virtualenv
```
创建一个 python 环境
```
virtualenv venv
```
激活环境
```
source bin/activate
```
退出虚拟环境
```
deactivate
```

## autoenv
如果目录包含 `.env` 文件，在切换目录的时候会自动激活虚拟环境

安装
```
sudo pip install autoenv
echo "source `which activate.sh`" >> ~/.bashrc
```
新建一个 `.env` 文件，添加激活命令
```
source ~/py/rpi/venv/bin/activate
```
## ref
http://docs.python-guide.org/en/latest/dev/virtualenvs/
