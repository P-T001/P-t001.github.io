# Find IP

---

原因：网站为了隐藏真实IP，做了CDN处理

1.判断目标是否做了CDN

- 多点ping

  （国内和国外都测试，如果一致代表真实IP，能看到每个IP的运营商是谁，如果是CDN运营商的基本就是CDN节点）

  ```
  http://tool.chinaz.com/speedtest/
  https://asm.ca.com/en/ping.php
  https://tools.ipip.net/newping.php 
  https://ping.aizhan.com/
  ```

- nslookup查CDN服务商

  ```
  nslookup
  www.xxx.com  # 如果出现多个解析证明做了CDN
  ```

- 查CDN服务商

  ```
  cloudflare.com
  akamai.com
  ```

  

2.寻找真实IP

- DNS历史解析

  域名开始绑定的时候可能是真实IP

  ```
  https://www.netcraft.com 
  http://www.who.is
  http://www.crimeflare.org/
  https://dnsdb.io/zh-cn/ ###DNS查询
  https://x.threatbook.cn/ ###微步在线
  http://viewdns.info/ ###DNS、IP等查询
  https://tools.ipip.net/cdn.php ###CDN查询IP
  http://fofa.so     # 搜特征
  ```

- 本地解析

  ```
  nslookup www.xxx.com
  ping www.xxx.com
  web 访问IP端口和域名的特征一致
  修改本地host 将IP指定域名，访问改域名跟没有指定的效果一样，则可以判断是真实IP
  ```

- 找子站IP

  ```
mail.xxx.com    # 自建邮件系统一般在内部，没有经过CDN
xxxxx.xxx.com   # 小的子站点可能不会做CDN，主站才会做
  ```



3.判断真实IP依据：

  ```
1.该IP只有几个域名指向的为真实IP    （CDN一般有1000个指向）
2.该IP运营商不为cdn运营商的为真实IP （通过ipip.net和微步x.threatbook.cn可以看到运营商）
3.在目标域名中注册账号，通过IP来访问登录成功，代表是真实IP
4.修改本地host 将IP指定域名，访问改域名跟没有指定的效果一样，则可以判断是真实IP
  ```

