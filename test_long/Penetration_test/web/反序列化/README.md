# 反序列化

---

介绍：

```
PHP使用一种人类可读的字符串格式，其中字母代表数据类型，数字代表每个条目的长度
```

user具有属性对象：

```
$user->name = "carlos"; $user->isLoggedIn = true;
```

序列化后：

```
O:4:"User":2:{s:4:"name":s:6:"carlos"; s:10:"isLoggedIn":b:1;}
```

可以解释如下：

```
O:4:"User" -具有4个字符的类名称的对象 “User"
2 -对象具有2个属性
s:4:"name" -第一个属性的键是4个字符的字符串 “name"
s:6:"carlos" -第一个属性的值是6个字符的字符串 “carlos"
s:10:"isLoggedIn" -第二个属性的键是10个字符的字符串 “isLoggedIn"
b:1 -第二个属性的值是布尔值 true
```

反序列化：

通过修改序列化后的属性和值达到漏洞的目的