# bypass waf

---

目录：

{% include list.liquid all=true %}

---

各种waf识别：（拦截图片）

```
https://www.cnblogs.com/AdairHpn/p/13985760.html
```

主流（牛批）服务waf：

```
D盾    （只能windows的IIS，但是可以伪装成apache、nginx等）
		后门检测-可以帮助hAck3r代码审计
宝塔   （linux和windows均可以装）
```

找waf特征：

```
1.查看页面源码
2.看request的header
```

waf特征内容：

```
360webscan    拦截页面：输入内容存在危险字符，安全起见，已被本站拦截
云锁           拦截页面：您所提交的请求含有不合法的参数，已被网站管理员设置拦截
D盾           拦截页面：D盾_拦截提示
UPUPW         拦截页面：您提交的内容存在危险字符，安全起见，UPUPW已拦截！如有问题请联系管理员解决

```

