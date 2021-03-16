# weipan

---

微盘框架特征：

```
网站标题的图标默认是绿色的微字（也可以在浏览器历史记录中查看）
用户在前端登陆后访问的是伪静态页面，如good/pid/2/token/xxxxxxx.html
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
数据库名
|-wp_userinfo  #用户表，管理员和用户信息存放的表
|--username用户名
|--upwd 密码md5
|--utime 注册时间戳，默认upwd是密码+utime的md5（具体需要看后台登陆页面是怎么校验登陆的）

```

