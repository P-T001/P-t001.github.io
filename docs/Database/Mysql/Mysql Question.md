# Mysql   Question

---

1.如果表中数据是超过一定位数的数字，导出会变成科学计数法

```
a -> concat('\t',a)   #将\t（制表符）和a 相连，转换成字符串数据类型
```

2.mysql不能远程访问

```
use mysql;
select host,user from user where user='root';  #查看user表
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%'IDENTIFIED BY '123456' WITH GRANT OPTION;      #修改为root@% 密码123456
flush privileges;                              #刷新权限
```

3.数据库乱码问题

```
show variables like'%char%' #查看数据库编码
set character_set_results=gb2312  #设置编码
```

4.navicat导入sql文件，数据乱码

```
使用记事本打开，另存为mysql的编码，再导入
```

