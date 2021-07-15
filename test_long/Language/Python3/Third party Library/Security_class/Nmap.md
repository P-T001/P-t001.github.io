# Nmap

---

## 准备环境

```
python3 windows下需要安装nmap和npcap程序
官网下载：https://nmap.org/download.html
nmap的安装包包含npcap程序，如果没有则要下载并安装npcap程序

下载最新的python-nmap库
手动下载并安装，也可以直接pip安装
http://xael.org/pages/python-nmap-0.6.1.tar.gz
解压后运行 python3 setup.py install
```

## 使用

```
端口扫描
import nmap
nm=nmap.PortScanner( )   # 创建端口扫描实例
ip='x.x.x.x'
nm.scan(hosts=ip,ports='21-33',arguments='-O' ) # ip,端口，nmap参数
nm.command_line()   # 获取nmap使用的命令
nm.scaninfo()       # 获取扫描的全部结果
nm.all_hosts()      # 获取扫描的主机列表
nm.csv()            # 输出扫描结果为csv样式的字符串类型
nm.has_host('x.x.x.x')  # 判断结果是否有ip存在
nm[ip].hostname()   # 扫描结果中ip的主机名
nm[ip].state()      # 扫描结果中ip的存活状态

主机扫描 使用参数-sn -PR


```

