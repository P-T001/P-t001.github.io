# bypass_disable_functions

---

介绍

```
使用蚁剑的插件“绕过disable_functions”
通过劫持外部程序来执行命令
只能针对linux系统
```

选择模式

```
LD_PRELOAD  通过修改环境变量来注入外部服务，如mail等

-
（教程：https://blog.csdn.net/kong_free/article/details/106891179）
通过phpinfo查看 server api ：FPM/FastCGI  即可通过该选项进行绕过
---
Fastcgi/PHP-FPM    选择Fastcgi方式进行绕过
unix:///tmp/php-cgi-56.sock #需要看php配置文件php/etc/php-fpm.conf #listen=/tmp/php-cgi-56.sock 	
php路径选择php
---
	会在当前目录生成.antproxy.php，使用蚁剑连接该文件（密码跟你一句话的密码一样）只有一会的时间就会断开，不稳定。（可以反弹shell到公网vps上进行持久化）
	如果有其他目录，没权限访问，在so路径下写入user.ini（open_basedir=:/）绕过php.ini的全局限制。

-
```

