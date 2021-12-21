# mysql Honeypot

---

利用脚本：

```
https://github.com/Gifts/Rogue-MySql-Server/blob/master/rogue_mysql_server.py
https://github.com/allyshka/Rogue-MySql-Server
```

步骤：

```
在脚本中定义filelist的文件列表，生成的日志mysql.log
自搭建服务器上运行rogue_mysql_server.py
等待别人连接服务器的mysql蜜罐 或者 通过网站漏洞连接该服务器mysql蜜罐也会触发
读取自定义的文件列表的内容输出到mysql.log
```

