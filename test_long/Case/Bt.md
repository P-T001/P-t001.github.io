# 宝塔

---

宝塔下载：

```
https://www.bt.cn/
```

宝塔控制:

```
/etc/init.d/bt  stop|start|restart   #停止|启动|重启
/etc/init.d/bt  default               #查看配置，面板端口、用户名、密码等
```

修改宝塔配置：

```
cd /www/server/panel && python tools.py panel 123456  #修改宝塔面板登陆密码
cd /www/server/panel && python tools.py root 123456   #修改宝塔数据库root密码
```

更加详细：

```
https://news.west.cn/65331.html
```

文件

```
default.db     # 登陆记录，从中发现宝塔界面账号密码
admin_path.pl  # 宝塔界面路径
default.pl     # 宝塔界面密码，如果登不上就看登陆记录文件
```

