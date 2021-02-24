# Cmd命令

---

常用命令：

```
certutil -hashfile 文件路径 MD5    # 校验文件哈希
tasklist /SVC                     # 查看进程
```

注册表操作

```
REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections # 查看RDP服务是否开启：1关闭，0开启

REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v PortNumber # 查看RDP服务的端口
```

