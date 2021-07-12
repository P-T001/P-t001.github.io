# x55_injection

---

目录：

{% include list.liquid all=true %}

类型：

dom型

存储型

反射型

x55平台：

```
https://www.mrwu.red/xss/
https://xss.pt/xss.php?do=login
```

xss能弹回真实IP，可以通过关闭WebRTC 功能来防止IP泄露

```
教程：https://blog.starryvoid.com/archives/274.html
```

```
Mozilla Firefox：在地址栏输入 “about:config”，搜索 “media.peerconnection.enabled” 并双击将值改为 “false”，WebRTC 将被关闭。

Google Chrome：在谷歌应用商店安装谷歌官方扩展 “WebRTC Leak Prevent”，在插件选项里找到 “IP handling policy:” 选择第三项 “Disable non-proxied UDP”，并点击下方 “Apply settings”

Google Chrome 另一种方法：在谷歌应用商店安装谷歌官方扩展 “WebRTC Network Limiter”，在插件选项里找到 “Options” 选择第四项 “Use my proxy server” 即可
```

