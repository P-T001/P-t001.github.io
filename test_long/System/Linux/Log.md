# Linux   log

---

**查看**

```
last          # 查看历史登陆记录，用户、IP
history       # 查看历史命令执行记录
w             # 查看当前登陆，用户、IP

```

**清除**

```
echo '' > /root/.bash_history                 #history记录
echo '' > /var/log/wtmp                       #last日志，查看历史登陆记录，用户、IP、时间
echo '' > /var/log/btmp                       #lastb日志 
echo '' > /var/log/lastlog                    #lastlog日志 ,查看所有用户登陆记录，IP只显示最近一次登陆
```

**组合命令**

```
查看历史登陆IP和端口（ubuntu：/var/log/auth*  ；centos：/var/log/secure*）:
(ls /var/log/auth*.gz|xargs zcat  |grep Accepted|awk '{print $1"/"$2,$3","$9","$11","$13}'  && ls /var/log/ |grep -E "secur|auth" |xargs cat  |grep Accepted|awk '{print $1"/"$2,$3","$9","$11","$13}') 2>/dev/null
```

**日志文件**

```
日志文件
/var/log/message 系统启动后的信息和错误日志，是Red Hat Linux中最常用的日志之一
/var/log/secure 与安全相关的日志信息
/var/log/maillog 与邮件相关的日志信息
/var/log/cron 与定时任务相关的日志信息
/var/log/spooler 与UUCP和news设备相关的日志信息
/var/log/boot.log 守护进程启动和停止相关的日志消息
/var/log/btmp – 记录所有失败登录信息  命令:lastb
/var/log/auth.log 系统授权信息，包括用户登录和使用的权限机制等 (debian)
/root/.bash_history  历史命令
```

**ssh登陆隐匿和伪装日志文件**
1.登陆账号不给管理员看到

```
ssh -T somebody@8.8.8.8 /bin/bash –i
```
2.不记录ssh公钥在本地.ssh目录中

```
ssh -o UserKnownHostsFile=/dev/null -T user@host /bin/bash –i
```


3.设置不纪录历史命令(.bash_history)

```
unset HISTORY HISTFILE HISTSAVE HISTZONE HISTORY HISTLOG; export HISTFILE=/dev/null; export HISTSIZE=0; export HISTFILESIZE=0
```

4.修改last命令
centos: 8.8.8.8-> 1.1.1.1

```
修改
utmpdump /var/log/wtmp |sed "s/8.8.8.8/1.1.1.1/g" |utmpdump -r >/tmp/wtmp1 &&\mv  /tmp/wtmp1 /var/log/wtmp
删除：
utmpdump /var/log/wtmp |sed "s/登录ip/d" |utmpdump -r >/tmp/wtmp1 &&\mv  /tmp/wtmp1 /var/log/wtmp
```

unix:192.168.8.88->/localhost

```
/usr/lib/acct/fwtmp < /var/adm/wtmpx | sed "s/192.168.8.88/localhost/g" | /usr/lib/acct/fwtmp -ic > /var/adm/wtmpx
```

5.修改lastlog

```
sed -i 's/192.168.1.1/8.8.8.8/g' /var/log/lastlog
```

6.删除当前时间日志

```
sed  -i '/当前时间/'d  /var/log/messages
```

7.覆盖文件次数31337

```
shred -n 31337 -z -u filename
```
**rootkit检测**

rootkit是一种特殊的恶意软件，它的功能是在安装目标上隐藏自身及指定的文件、进程和网络链接等信息，比较多见到的是Rootkit一般都和木马、后门等其他恶意程序结合使用

- 来源：https://blog.csdn.net/guancong3412/article/details/88535331

- 1.chkrootkit

   ```
   wget ftp://ftp.pangeia.com.br/pub/seg/pac/chkrootkit.tar.gz
   tar xf chkrootkit.tar.gz
   cd chkrootkit-0.52/
   ./chkrootkit |grep INFECTED
   ```

- 2.rkhunter

  ```
  wget http://jaist.dl.sourceforge.net/project/rkhunter/rkhunter/1.4.2/rkhunter-1.4.2.tar.gz
  ./installer.sh --install
rkhunter --update # 扫描之前最好更新病毒库
  rkhunter -c --sh
  yum install rkhunter -y
  rkhunter
  –checkall (-c) #全系统检测，rkhunter的所有检测项目;
  –createlogfile #建立登录档，一般预设放在/var/log/rkhunter.log;
  –skip-keypress #忽略按键后继续的举动(程序会持续自动执行);
  –versioncheck #检测试否有新的版本在服务器上;
  接下来运行rkhunter --checkall，连续敲击回车，数分钟后得到报表
  rkhunter --checkall
  rkhunter --check --sk  # --checkall ,不用连续敲击回车
  
  ```
  
- LinuxCheck
  
  ```
  https://github.com/al0ne/LinuxCheck
  ```
  
  