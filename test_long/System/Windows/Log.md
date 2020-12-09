# Windows  log

---

## 查看

```
快捷键：win+r   
eventvwr.exe
有应用程序、安全、setup、系统等
```



## 备份

```
C:\windows\system32\winevt\logs\*.evtx
```







## 清除

部分清除

原理：先筛选（排除自己想删除的）然后再覆盖原本的日志文件

1.根据日志ID排除生成新日志（powershell）

```
wevtutil epl Security C:\Windows\System32\winevt\Logs\Security_new.evtx /q:"*[System[(EventRecordID!=6810)]]" /ow:true
```



2.根据IP排除生成新日志（powershell）

```
wevtutil epl Security C:\Windows\System32\winevt\Logs\Security_new.evtx /q:"*[EventData[(Data[@Name='IpAddress']!='127.0.0.1')]]" /ow:true
```



完全删除（cmd和powershell均可）

```
del  C:\Windows\System32\winevt\Logs\Security.evtx（日志路径，有三个）
也可以图形界面在事件查看器，右键日志清除日志
```



