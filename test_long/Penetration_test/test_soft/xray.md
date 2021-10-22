# xray

---

- - 官网：https://docs.xray.cool/
- - 下载 ：https://github.com/chaitin/xray

与burp联动被动扫描：
```
xray webscan --listen 127.0.0.1:7777 --html-output proxy.html
burp设置代理为目标：*xxx.com* 代理：127.0.0.1:7777
```

配置文件：config.yaml

```
http:
  proxy:"http://127.0.0.1:10809"
  max_qps:200      # 每秒最大请求数
```





PS：

什么地方不要使用xray，管理后台，发帖等，会产生记录或者服务器崩溃