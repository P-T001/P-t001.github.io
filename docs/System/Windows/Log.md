# Windows  log

---

## 查看

```
快捷键：win+r   
eventvwr.exe
有应用程序、安全、setup、系统等
```

---

## 备份

```
C:\windows\system32\winevt\logs\system.evtx      #系统日志
C:\windows\system32\winevt\logs\setup.evtx       #setup日志
C:\windows\system32\winevt\logs\security.evtx    #安全日志
C:\windows\system32\winevt\logs\Application.evtx #应用程序日志
```

---

## 日志分析

| 日志     | 事件ID                                         | 动作                                                   |
| -------- | ---------------------------------------------- | ------------------------------------------------------ |
| 安全日志 | 4624（存在登陆IP）                             | 远程登陆成功                                           |
| 安全日志 | 4625                                           | 远程登陆失败                                           |
| 安全日志 | 4634                                           | 登陆注销                                               |
| 安全日志 | 4776（凭据验证）、4648、4624、4672（特殊登陆） | 使用超级用户（如管理员）进行登录，会同时产生四个时间ID |
| 安全日志 | 1102                                           | 日志清除                                               |





---

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



