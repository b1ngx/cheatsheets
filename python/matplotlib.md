# matplotlib

解决 matplotlib 不支持中文的问题

找出系统安装的中文字体

```python
import matplotlib

%matplotlib inline

ttfs = sorted([f.name for f in matplotlib.font_manager.fontManager.ttflist])

for t in ttfs:
    print(t)
```

设置 plt.rcParams['font.family'] 为系统安装的字体

```py
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

%matplotlib inline

# 结局中文乱码
# https://blog.csdn.net/gmr2453929471/article/details/78655834
plt.rcParams['font.family']=['Source Han Serif CN']

df = pd.DataFrame(np.random.randn(1000, 4), columns=list('ABCD'))
df = df.cumsum()

plt.figure()

df.plot(title="折线图",figsize=(10,6))
```

参考：https://blog.csdn.net/gmr2453929471/article/details/78655834
