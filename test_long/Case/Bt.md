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
/www/server/panel/data/default.db     # 登陆记录，从中发现宝塔界面账号密码
/www/server/panel/data/admin_path.pl  # 宝塔界面路径
/www/server/panel/data/default.pl     # 宝塔界面密码，如果登不上就看登陆记录文件
/www/server/panel/data/port.pl  # 面板端口
/www/server/panel/data/domain.conf  # 域名绑定面板
/www/server/panel/data/*.login    # 登陆限制
/www/server/panel/data/limitip.conf  # 面板授权IP
```

宝塔面板

```
通过计划任务执行cs马拿到服务器权限
```

aapanel（国际版BT）-远程代码执行

```
https://github.com/jenaye/aapanel
```

