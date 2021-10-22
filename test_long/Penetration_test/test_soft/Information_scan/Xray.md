# Xray

---

扫描漏洞，生成报告

---

**下载**

```#
https://github.com/chaitin/xray/releases
```

---

**使用**

浏览器代理端口设置7777进行被动扫描(浏览器设置代理下述本地端口，进行被动扫描)

```
xray.exe webscan --listen 127.0.0.1:7777 --html-output output.html  
```

单个扫描，不使用爬虫

```
xray.exewebscan --url http://example.com/?a=b --html-output single-url.html
```

使用爬虫扫描

```
xray.exewebscan --basic-crawler http://example.com --html-output vuln.html
```

**配置**

```
具体见手册：https://docs.xray.cool/#/configration/README
config.yaml为配置文件
#---
proxy: "http://127.0.0.1:10809"
```

