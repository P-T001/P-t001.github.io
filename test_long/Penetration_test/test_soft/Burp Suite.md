#  Burp Suite

---

## 安装

运行环境：

```
v2020.4以上版本需要java9以上：（jdk-9_windows-x64_bin.exe）
https://www.oracle.com/technetwork/cn/java/javase/downloads/jdk9-downloads-3848520-zhs.html
v2020.4以下版本需要java8：（jdk-8u271-windows-x64.exe）
https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html
```

运行文件：

```
burp-loader-keygen.jar  # 注册机
burpsuite_pro.jar       # burp主程序
BurpSuiteCn.jar         # 汉化包
```

汉化运行：（以下保存为“.bat”，跟上述三个文件放在一起）

```
java -noverify -javaagent:BurpSuiteCn.jar -Dfile.encoding=utf-8  -Xbootclasspath/p:burp-loader-keygen.jar -jar burpsuite_pro.jar
```

---

## 使用

代理/选项/代理监听器

```
127.0.0.1:8080    # 如果只在本地抓包，开这个即可
IP:8080           # 如果要抓其他设备的包需要设置本地IP，然后其他设备设置代理为这个IP和端口
```

用户选项/连接/顶级代理服务器

```
设置代理IP和端口，burp的流量都走该代理
```





---

## 问题

1.正常能访问，但使用burp拦包后，网站403不能访问资源

原因：网站使用http 2.0协议，不能拦截包

解决：使用HttpCanary监控网络包，然后修改内容进行重放（本质不会拦截网络包）

