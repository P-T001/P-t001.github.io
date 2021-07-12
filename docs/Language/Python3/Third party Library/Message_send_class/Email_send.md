# Email_send

---

**前提**：(需要smtp服务，可以本地搭，也可以使用第三方QQ、网易等)

第三方QQ：设置/邮箱设置/账户/SMTP服务/生成授权码 /（全部都开启） 

**代码**：

```
import yagmail   

#参数
user = 'xxxx0@qq.com'  # 发送账号
password = 'xxxxxxxx' # 授权码，需要绑定手机发短信进行开通,开通后会显示授权码（只显示一次记得保存）
receive = ['xxxx1@qq.com','xxxx2@qq.com']  # 接收地址列表
report = [r'x1.txt',r'x2.txt']             # 发送的附件路径列表

smtp = yagmail.SMTP(user=user,             # 发送邮箱
                    password=password,     # 发送邮箱密码
                    host='smtp.126.com',   # smtp地址，发送账号使用什么账号就使用对应的smtp地址
                    smtp_ssl=True)

smtp.send(to=receive,                      # 接收人
          subject='我是邮件标题',           # 邮件标题
          contents='我是邮件正文',          # 邮件正文
          attachments=report               # 附件
          )
          
smtp.close()

print('发送成功')
```

