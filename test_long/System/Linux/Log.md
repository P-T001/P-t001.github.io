# Linux   log

---

## 查看

```
last          # 查看历史登陆记录，用户、IP
history       # 查看历史命令执行记录
w             # 查看当前登陆，用户、IP

```

## 清除

```
echo '' > /root/.bash_history                 #history记录
echo '' > /var/log/wtmp                       #last日志，查看历史登陆记录，用户、IP、时间
echo '' > /var/log/btmp                       #lastb日志 
echo '' > /var/log/lastlog                    #lastlog日志 ,查看所有用户登陆记录，IP只显示最近一次登陆
```

## 组合命令

```
查看历史登陆IP和端口（ubuntu：/var/log/auth*  ；centos：/var/log/secure*）:
(ls /var/log/auth*.gz|xargs zcat  |grep Accepted|awk '{print $1"/"$2,$3","$9","$11","$13}'  && ls /var/log/ |grep -E "secur|auth" |xargs cat  |grep Accepted|awk '{print $1"/"$2,$3","$9","$11","$13}') 2>/dev/null
```

