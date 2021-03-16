# sudo

---

介绍：

```
2021.1.26 Sudo发布安全通告，修复了一个类Unix操作系统在命令参数中转义反斜杠时存在基于堆的缓冲区溢出漏洞。当sudo通过-s或-i命令行选项在shell模式下运行命令时，它将在命令参数中使用反斜杠转义特殊字符。但使用-s或 -i标志运行sudoedit时，实际上并未进行转义，从而可能导致缓冲区溢出。只要存在sudoers文件（通常是 /etc/sudoers），攻击者就可以使用本地普通用户利用sudo获得系统root权限。请受影响的用户尽快采取措施进行防护。
CVE-2021-3156-sudo
PS：centos不支持（cat /etc/redhat-release查看系统版本）
```

版本：

```
sudo -V   # 查看版本
影响：
Sudo 1.8.2 - 1.8.31p2
Sudo 1.9.0 - 1.9.5p1
不影响：
Sudo =>1.9.5p2
```

测试：

```
非root账号登陆：sudoedit -s /  
出现“sudoedit：”报错则存在影响
出现“usage：”报错则不存在影响
```

修复：(使用阿里云镜像源，执行修复命令)

```
yum update sudo
```

