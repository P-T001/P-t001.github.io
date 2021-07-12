# Third party Library

---

目录：

{% include list.liquid all=true %}

---

**国内镜像源**

```
清华：https://pypi.tuna.tsinghua.edu.cn/simple

阿里云：https://mirrors.aliyun.com/pypi/simple/

中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/

华中理工大学：https://pypi.hustunique.com/

山东理工大学：https://pypi.sdutlinux.org/ 

豆瓣：https://pypi.douban.com/simple/
```

**临时换源安装**

```
pip install xxx -i 镜像源地址
```

**指定版本安装**

```
pip install xxx==0.0.1
```

**永久换源**

```
路径：c:/用户/用户名/pip.ini
---
[global]
timeout = 6000
index-url = https://pypi.tuna.tsinghua.edu.cn/simple
trusted-host = pypi.tuna.tsinghua.edu.cn
```

