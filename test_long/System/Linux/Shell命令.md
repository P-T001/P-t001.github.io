# Shell命令

---

常用命令：

```
netstat -tnlp   # 查看端口
ps aux|grep 进程名   #筛选进程相关信息
df -h                #看挂载目录大小
du -sh *             #看当前的所有文件大小
find
grep
curl -x socks5h://127.0.0.1:4444 https://www.sougou.com/   # 使用代理去访问搜狗
arch  # 看cpu 架构
cat /proc/cpuinfo # 看cpu 详细信息
cat /proc/cpuinfo |grep name | cut -f2 -d: |uniq -c #只能cpu
```

代理设置：

```
ProxyChains：
/etc/proxychains.conf 
---
socks5  x.x.x.x 端口
---
proxychains  运行命令  命令参数   # 走代理使用命令

```

