# Potato

---

 （针对本地服务型用户，而且不能用于域用户、普通用户）

```
教程：http://hackergu.com/powerup-stealtoken-rottenpotato/
下载：
https://github.com/SecWiki/windows-kernel-exploits/blob/master/MS16-075/potato.exe
https://github.com/breenmachine/RottenPotatoNG/blob/master/RottenPotatoEXE/x64/Release/MSFRottenPotato.exe
https://github.com/foxglovesec/RottenPotato
```

原理：

```
1.欺骗 “NT AUTHORITY\SYSTEM”账户通过NTLM认证到我们控制的TCP终端。
2.对这个认证过程使用中间人攻击（NTLM重放），为“NT AUTHORITY\SYSTEM”账户本地协商一个安全令牌。这个过程是通过一系列的Windows API调用实现的。
3.模仿这个令牌。只有具有“模仿安全令牌权限”的账户才能去模仿别人的令牌。一般大多数的服务型账户（IIS、MSSQL等）有这个权限，大多数用户级的账户没有这个权限。
```

