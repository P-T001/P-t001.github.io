# Server

---

linux服务器取证：

打包日志：

```
mkdir  /log
history > /log/history.log  #备份历史命令
last > /log/last.log    #备份历史登陆日志
其他的一些日志、涉案服务的版本等
cp -r /www/server/panel/logs/request /log  #宝塔的请求日志目录
cp -r /www/wwwlogs   /log                  #web 访问日志
```

基础命令

```
netstat -tnlp        #看端口
ps aux|grep 进程名   #筛选进程相关信息
df -h                #看挂载目录大小
du -sh *             #看当前的所有文件大小
```

打包文件：

```
tar cfzv 压缩后文件路径 需要压缩的文件路径       #使用tar打包成gz格式文件
tar cfz 压缩后文件路径 需要压缩的文件路径 --exclude=排除路径1  --exclude=排除路径    # 排除目录打包
tar cfz 压缩后文件路径 需要压缩的文件路径 --exclude=*.jpg  --exclude=*.png         # 排除文件类型打包
tar cfz 压缩后文件路径 需要压缩的文件路径1 需要压缩的文件路径2                       # 指定多个路径打包
tar cfz 压缩后文件路径 需要压缩的文件路径/*.jpg 需要压缩的文件路径/*.png             # 筛选文件类型打包
参数：
c 压缩
f 指定文件
z gz格式
v 输出详细打包文件路径
```

解压文件：

```
tar xfzv tar.gz的压缩包路径                    #解压tar打包的gz格式文件
参数：
x 解压
```

后台运行：

```
nohub 命令  &
```

找数据库连接文件：

```
grep -r -i -e 'db_user|db_host|db_password' 搜索路径       #搜索 数据库连接主机、用户、密码
参数：
-r 递归路径
-i 不区分大小写，默认区分
-e 拓展支持正则表达式
```

数据库绕过密码：

```
systemctl stop mysql  #停止mysql服务
mysqld_safe --skip-grant-tables & mysql   #跳过权限认证运行mysql
```

或者

```
vim /etc/my.cnf
–-skip-grant-tables   

systemctl restart mysql #重启mysql服务
```

修改数据库密码：

```
use mysql； #切换到mysql库
update user set password=password("123456") where user='root'; #修改root密码
flush privileges; #更新权限
exit退出
mysql -uroot -p123456   #连接mysql
show databases;         #查看所有数据库
```



数据库打包：

```
mysql --version > /log/mysql_version.log   #记录数据库版本
mysql -uroot -pxxxx -h 主机IP -E 'select version();' #远程连接mysql显示版本
mysqldump -uroot -pxxxx -h 主机名IP --databases 库名1 库名2   > /log/xxx.sql      #
```

