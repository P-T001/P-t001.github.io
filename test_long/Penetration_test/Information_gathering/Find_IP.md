# Find IP

---

原因：网站为了隐藏真实IP，做了CDN处理

判断IP是否做CDN，查IP的运营商看是否是做CDN服务

```
cloudflare.com
akamai.com
```





1.多地ping（国内和国外都测试，如果一致代表真实IP）

```
http://tool.chinaz.com/speedtest/
https://asm.ca.com/en/ping.php
https://tools.ipip.net/newping.php  
```



2.DNS历史解析

域名开始绑定的时候可能是真实IP

```
https://www.netcraft.com 
http://www.who.is
http://www.crimeflare.org/
```



3.本地解析

```
nslookup www.xxx.com

ping www.xxx.com

web 访问IP端口和域名的特征一致

修改本地host 将IP指定域名，访问改域名跟没有指定的效果一样，则可以判断是真实IP
```



4.mail系统

```
mail.xxx.com    # 自建邮件系统一般在内部，没有经过CDN
```



判断真实IP依据：

```
1.该IP只有几个域名指向的为真实IP    （CDN一般有1000个指向）
2.该IP运营商不为cdn运营商的为真实IP （通过ipip.net和微步x.threatbook.cn可以看到运营商）
```



