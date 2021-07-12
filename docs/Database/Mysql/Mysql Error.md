# Mysql  Error

---

1、ERROR 2002 (HY000): Can’t connect to local MySQL server through socket ‘/var/lib/mysqld/mysqld.sock’

```
原因：安装mariadb时，mysqld.sock安装在/tmp/下，因为yum安装是根据php、mysql组合的，

解决：ln -s /tmp/mysqld.sock  /var/lib/mysqld/mysqld.sock
```

2、ERROR 1045 (28000): Access denied for user 'root'@'localhost' (using password: NO)

```
原因：/etc/my.cnf 文件的内容没有定义
basedir=/usr/local/mysql
datadir=/data/mysql
socket=/tmp/mysql.sock

解决：
也可以这样
编辑 /etc/my.cnf 写入skip-grant-tables   #修改密码后注释掉，并重启服务
重启mysql服务
mysql -uroot #连接
update mysql.user set authentication_string=password('123456') where user='root' ;     #修改密码
```

3、ERROR! MySQL server PID file could not be found!

```
原因：service mysql restart  提示

service mysql start 即可
```

4、ERROR！Can 't connect to local MySQL server through socket '/tmp/mysql.sock '(2) ";

```
原因：找不到/tmp/mysql.sock ，

解决：find / -name mysql.sock

数据库目录的配置如：/var/local/data/mysql/下的my.cnf修改socker的路径

成查找到的路径
```

5、2059 - Authentication plugin 'caching_sha2_password' cannot be loaded:

```
原因：mysql8.0 的最新mysql_native_password加密方式在客户端不支持

use mysql;

select user,plugin from user where user='root';  #查看root的密码加密方式

alter user 'root'@'%' identified with mysql_native_password by ''; #修改加密方式和密码
```

6、ERROR 1290 (HY000): The MySQL server is running with the --skip-grant-tables option so it cannot execute this statement

```
使用刷新权限即可，执行其他命令

flush privileges;
```

7、[Err] 1194 - Table 'order' is marked as crashed and should be repaired

```
原因是数据库服务是拉取的，整个索引坏了，要重新检查索引

mysql的bin下使用

myisamchk -c -r ../data/tablename/*.MYI
```

8、ERROR 1030 (HY000): Got error -1 from storage engine

```
my.ini配置文件
innodb_force_recovery  选项注释 #该选项是安全选项，数据库都是只读的
```

9、1194 - Table 'xxx' is marked as crashed and should be repaired

```
use 数据库;
REPAIR TABLE `xxx`;
或
myisamchk  -c -r ./xxx.MYI 
```

10、1045-Access denied for user 'root'@'localhost'（using password: YES）

```
\>use mysql

\>UPDATE user SET Password=PASSWORD('') where USER='root';

\>FLUSH PRIVILEGES;
```

