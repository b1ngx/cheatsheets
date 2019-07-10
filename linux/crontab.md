# crontab
定时任务

## crond

crond 是 linux下用来周期性的执行某种任务或等待处理某些事件的一个守护进程.

查看服务状态

```
systemctl status crond
```

## command
![](media/15627253658195.jpg)


用户所建立的crontab文件中，每一行都代表一项任务，每行的每个字段代表一项设置，它的格式共分为六个字段，前五段是时间设定段，第六段是要执行的命令段。

在以上各个字段中，还可以使用以下特殊字符：

- 星号（*）：代表所有可能的值，例如month字段如果是星号，则表示在满足其它字段的制约条件后每月都执行该命令操作。

- 逗号（,）：可以用逗号隔开的值指定一个列表范围，例如，“1,2,5,7,8,9”

- 中杠（-）：可以用整数之间的中杠表示一个整数范围，例如“2-6”表示“2,3,4,5,6”

- 正斜线（/）：可以用正斜线指定时间的间隔频率，例如“0-23/2”表示每两小时执行一次。同时正斜线可以和星号一起使用，例如*/10，如果用在minute字段，表示每十分钟执行一次。

## 环境变量

有时我们创建了一个 crontab，但是这个任务却无法自动执行，而手动执行这个任务却没有问题，这种情况一般是由于在 crontab 文件中没有配置环境变量引起的。

所以你要保证在shelll脚本中提供所有必要的路径和环境变量，除了一些自动设置的全局变量。所以注意如下3点：

1. 脚本中涉及文件路径时写全局路径；

2. 脚本执行要用到java或其他环境变量时，通过source命令引入环境变量，如：

    ```
    cat renew.sh
    
    #!/bin/sh
    
    source /etc/profile
    
    python -c 'import random; import time; time.sleep(random.random() * 3600)' && certbot renew

    ```

3. 当手动执行脚本OK，但是crontab死活不执行时。这时必须大胆怀疑是环境变量惹的祸，并可以尝试在crontab中直接引入环境变量解决问题。如：

    ```
    0 0,12 * * * . /etc/profile; python -c 'import random; import time; time.sleep(random.random() * 3600)' && certbot renew
    ```

## 参考
[每天一个linux命令（50）：crontab命令](https://www.cnblogs.com/peida/archive/2013/01/08/2850483.html)

