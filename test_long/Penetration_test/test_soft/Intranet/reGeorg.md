# reGeorg

---

- 介绍

利用http/https隧道进行内网穿透，动静太大，会拖垮web端访问

- 链接：https://github.com/sensepost/reGeorg

- 使用

  ```
  1.将对应的tunnel上传（看服务器支持哪种语言运行）
  2.本地运行，绑定本地8080端口，连接目标隧道文件
  python reGeorgSocksProxy.py -p 8080 -u http://upload.sensepost.net:8080/tunnel/tunnel.jsp
  3.将流量代理到本地8080端口，使用Proxifier软件即可
  ```

  

