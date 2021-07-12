# HttpCanary

---

### 介绍：

```
HTTP/HTTPS/HTTP2网络包抓取和分析工具,安卓手机上的一个抓包工具
```

### 插件：

```
HttpCanary -> 设置 -> 插件管理 -> 右上角+号 -> 插件仓库
1.Host屏蔽（/HttpCanary/plugins/HostBlock/目录下），是否需要加端口号，看包内容的host:IP后面是否有端口号
www.hello.com
www.work.com
www.bug.com:8080
10.11.12.13
10.10.10.10
123.123.123.123
---
2.MimeType屏蔽(/HttpCanary/plugins/MimeTypeBlock/目录下),res-mimes.txt为屏蔽响应包
video/mp4
image/jpeg
---
3.图片、音频、视频下载器
通过匹配Content-Type是否为图片、音频、视频来进行保存
---
4.请求统计表
将抓包的请求信息以excel表格式输出
---
5.微信定位漂移
通过http://api.map.baidu.com/lbsapi/getpoint/index.html获取经纬度，粘贴到设置中


```

