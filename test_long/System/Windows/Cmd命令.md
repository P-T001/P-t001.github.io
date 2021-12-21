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

查看wifi连接信息(关键内容:wifi密码)

```
for /f  "skip=9 tokens=1,2 delims=:" %i in ('netsh wlan show profiles')  do  @echo %j | findstr -i -v echo |  netsh wlan show profiles %j key=clear
```

软件系统信息：

```
wmic OS get Caption,CSDVersion,OSArchitecture,Version  # 查看系统版本：
wmic product get name,version   # 查看安装的软件：(获取得比较慢)
```

找端口进程对应文件路径

```
netstat -ab # 查看端口和进程名
tasklist # 查看进程pid   
wmic process # 查看进程路径 
|findstr "xx"  # 对前面命令输出进行管道筛选
```

修改cmd乱码显示

```
chcp 65001         # 修改成utf-8
```

获取当前时间戳

```
powershell -c Get-Date -Format yyyyMMddHHmmssfff
```

清除windows日志（需要超级管理员权限）

```
wevtutil cl security             # 清除安全日志
wevtutil cl system               # 清除系统日志
wevtutil cl application          # 清除应用程序日志
wevtutil cl "windows powershell" # 清除powershell日志
```

