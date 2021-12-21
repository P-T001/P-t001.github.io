# windows 提权

---

辅助提权-查询：

通过windows系统的命令，将结果粘贴到下面的链接中

```
systeminfo
http://payloads.net/Windows_patch/
https://i.hacking8.com/tiquan/
http://blog.neargle.com/win-powerup-exp-index/#
```

辅助提权poc：

```
https://github.com/SecWiki/windows-kernel-exploits
```

杀软识别：

```
tasklist /svc
http://ddoslinux.com/windows/index.php
http://payloads.net/kill_software/
```

**烂土豆**（MS16-075）（针对本地用户）

```
原理：
欺骗 “NT AUTHORITY\\SYSTEM”账户通过NTLM认证到我们控制的TCP终端。
对这个认证过程使用中间人攻击（NTLM重放），为“NT AUTHORITY\\SYSTEM”账户本地协商一个安全令牌。这个过程是通过一系列的Windows API调用实现的。
模仿这个令牌。只有具有“模仿安全令牌权限”的账户才能去模仿别人的令牌。一般大多数的服务型账户（IIS、MSSQL等）有这个权限，大多数用户级的账户没有这个权限。

优点：
100%可靠
全版本通杀
立即生效，不用像hot potato那样有时候需要等Windows更新才能使用。

需要配合msf
```



**多汁土豆**（针对本地用户）

```
https://github.com/ohpe/juicy-potato
在本地账户的权限下
1.以system权限加载COM请求，认证NTLM（当然我们是本地账户，无法越权使用system权限，会认证失败）

2.再以本地账户权限发起默认135端口请求，认证NTLM（这次权限对了认证成功了）

3.分别拦截两个NTLM的数据包，替换数据，使得通过步骤1的认证，获得system权限的token

4.利用system权限的token创建进程
```

