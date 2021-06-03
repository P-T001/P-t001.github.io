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

设置cmd走代理

```
set http_proxy=http://127.0.0.1:10809 
set https_proxy=http://127.0.0.1:10809
```

查询本电脑历史插入u盘记录：

```
reg query HKLM\System\currentcontrolset\enum\usbstor /s >c:\usb.txt  
使用“FriendlyName”作为关键词查找即可，此为u盘设备名称。
```

关闭windows防火墙

```
netsh firewall set opmode mode=disable
```

