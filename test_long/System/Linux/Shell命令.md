# Shell命令

---

- 常用命令：

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
type *.txt > /root/1.txt     //合并当前目录下的所有 txt 文件内容到 1.txt
cat 1.txt|sort|uniq > 2.txt    //去掉 1.txt 的重复内容并写入到 2.txt
find -type f -name '*.php'|xargs grep 'xxx' # 查找php文件，内容含xxx
```

- grep

```
grep xxx    # 包含
grep -v xxx # 排除
awk '{print $2}' # 只显示前者输出的第二列
xargs –I {} kill -9 {} # 将前者的输出作为参数执行，kill杀死进程
例子：
ps -ef |grep -v grep |grep mysql |awk '{print $2}'  # 显示mysql进程的pid（输出的第二列是pid）
ps -ef |grep -v grep |grep mysql |awk '{print $2}'|xargs –I {} kill -9 {}  # 批量杀死mysql进程
```

- 代理设置

```
ProxyChains：
/etc/proxychains.conf 
---
socks5  x.x.x.x 端口
---
proxychains  运行命令  命令参数   # 走代理使用命令

```

