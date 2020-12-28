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

还原：

```
use 数据库;
source /路径/xxx.sql;
```



