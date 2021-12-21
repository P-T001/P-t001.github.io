# Mysql  Backup

---

mysql主流引擎

```
MyiSAM：frm(存储表结构)、MYD(存储表数据)、MYI(存储表索引)
InnoDB：frm(存储表结构)、ibd（存储表数据）
MEMORY：（不常用）
```

mysql物理备份工具：

```
xtrabackup  #mysql官方，对任何引擎的数据库进行备份和还原
```

备份分类：

```
热备份：数据库运行时进行命令备份，恢复时要创建一个数据库并使用在备份，原理：将备份前的操作运行一次，较快
冷备份：数据库关闭时进行物理备份，直接恢复即可，原理：将关键性文件备份，较慢
```

备份：

```
mysqldump -u用户名 -p密码 --databases 库名1 库名2 > /路径/xxx.sql
mysqldump -u用户名 -p密码 --databases 库名1 库名2 |gzip > /路径/xxx.sql.tar.gz  #进行压缩备份
```

还原：（还原时需要对应数据库版本，最好能最精确到小版本，一般大版本也可）

```
use 数据库;
source /路径/xxx.sql;
```

恢复删除的数据

```
show variables like 'log_bin';         # 查看binlog日志状态,Value"为"ON”表示已开启。
show master status;                    # 找到当前mysql记录的binlog文件,如'binlog.000001'
show binlog events in 'binlog.000001'; # 查看binlog日志，定位原因
mysqlbinlog --no-defaults binlog.000001 >001bin.sql  # 命令 将二进制文件binlog导出成sql文件
从此文件中可以看出创建数据库、创建表、设计表、添加表数据，删除数据的所有SQL语句，接下来的工作可以使用此创建数据库和数据库表部分的语句，插入表内容的语句进行数据库恢复工作（需要定位create table 目标表名）
如果未开启binlog日志状态，使用Percona Data Recovery Tool for InnoDB工具进行恢复，但恢复比较有限
```

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     

