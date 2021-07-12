# AntSword

---

## 中国蚁剑

PS：使用加载器加载源码即可

```
源  码 ：https://github.com/AntSwordProject/antSword
加载器 ： https://github.com/AntSwordProject/AntSword-Loader
```

注意事项：

```
编辑数据/其他设置/忽略https证书 （勾选）
系统设置/代理设置/（设置代理）
```

修改header特征：

```
编辑数据/请求信息/(暂时修改为chrome的header)
	User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.72 Safari/537.36
---
也可以通过修改配置进行永久修改
/modules/request.js
const USER_AGENT = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.72 Safari/537.36 '
```

流量加密

```
编码设置/新建编码器or解码器 进行流量包的加密
```

可加载插件