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

