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

定点提取

```
substr('0123456',start,length)
start：开始序号
length：提取长度，不填则选择后面全部
```

编码

```
chr(16进制/10进制)   # 返回整数对应的ascii字符  #chr(0x61)->a  或者chr(97)->a
base64_decode()     # base64解密  # base64_encodebase64加密
str_rot13()         # rot13编码，每个字母向前移动13位，
				  # I love Shanghai <=>V ybir Funatunv 相互转换
				   
```

