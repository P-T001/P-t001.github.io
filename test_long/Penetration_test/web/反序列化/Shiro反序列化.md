# Shiro反序列化

---

介绍：

```
shiro是java的安全框架,执行身份验证、授权、密码和会话管理等的api。
影响版本：Shiro<=1.2.4反序列化
```

利用工具：

```
https://github.com/feihong-cs/ShiroExploit  # Shiro漏洞利用工具
https://github.com/sv3nbeast/ShiroScan      # 漏洞扫描
https://github.com/j1anFen/shiro_attack     # Shiro漏洞利用工具注入内存马
```

检测：

```
1.发生在登陆处，在返回包cookie里面出现：remenberMe=deleteMe
2.发生在登陆处，在请求包cookie后面加;remenberMe=deleteMe，返回包也会出现remenberMe=deleteMe
```

操作步骤：
```
https://www.anquanke.com/post/id/227090
```

