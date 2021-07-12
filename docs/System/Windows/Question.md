# Windows    Question

---

1.蓝屏解决

下载bluesreenview查看系统蓝屏原因（dump文件）

1.ntoskrnl.exe出现错误

```
1.使用 DirectX修复工具增强版 修复系统文件
2.管理员运行cmd：
chkdsk c: /f    
y
重启后对系统盘进行修复
看运气，能自动修复就可以
```

2.window10关闭自动更新

```
服务：
	运行services.msc  ，windows update 停用并禁用，恢复无操作
组策略
	运行gpedit.msc ，计算机配置/管理模板/windows组件/windows更新/配置自动更新 禁用
```



