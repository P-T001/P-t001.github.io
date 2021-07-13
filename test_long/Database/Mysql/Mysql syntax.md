# Mysql  语法

---

## 数据库操作：

```
create database 库名;     # 创建数据库
drop database 库名;       # 删除数据库
show databases 库名;      # 查看所有数据库
use 库名;                 # 使用该数据库
```

---

## 表操作：

创建表：

```
create table 表名 (列名1 数据类型 属性,列名2 数据类型 属性,....)    
	可选属性：
		Not NULL 不能为空，AUTO_INCREMENT 自动增长，DEFAULT NULL默认为空，COMMENT'备注'
		PRIMARY KEY(·id·) #以id为主键
	数据类型：
		chat、int、logtext、time、date等

```

删除表：

```
drop table 表名;    
```

查看所有表：

```
show tables;
```

插入表：

```
insert into 表名(字段名1,字段名2,...) values('值1','值2',...);
```

更新表：

```
update 表名 set 字段名='值' where (条件);
```

查询表：

```
select * from 表名;
	where(条件) 可and(&&)/or(||)
		字段名 = ''                       #精确匹配，|!= 不等于，>大于 ，<小于
		字段名 like '%值%'                #模糊匹配。_单词字符匹配，%任意字符匹配
		字段名 REGEXP '正则表达式'         #正则匹配
		字段名 in (x1,x2,x3)              #多项精确匹配，|not in 不等于
		length(字段名) between n and m    #字段长度在n-m之间
	group by 字段名   #以该字段名分组
		having 条件  #对分组后的结果进行条件筛选
	order by  字段名(以该字段排序) desc降序/asc升序(默认),....  #可进行多个字段排序
	limit n m        #对查询结果从n位开始，显示m个
		
select id,name from 表1 union select id,name from 表2  #联合查询，字段个数要一致，新的字段名以第1个为准
```

---

## 字段操作

注释符：

```
-- 注释内容    (PS：注意空格)
/*注释内容*/
#注释内容
```

字段：

```
FROM_UNIXTIME()   #时间戳 -> 时间
INET_ATON()       #ip地址 -> 数字型地址
INET_NTOA()       #数字型地址 -> ip地址
length()          #长度
sum()             #累加数值
count()           #count(*)统计行数(null不排除)、count(distinct 字段名)统计该列不同值个数(null排除)
```

