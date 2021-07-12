#  Burp Suite

---

**安装**

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

**使用**

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
 **插件**

- 安装插件教程：https://blog.csdn.net/weixin_40412037/article/details/103648034

- captcha-killer ：验证码识别

  ```
  安装burp插件：https://blog.csdn.net/xiayu729100940/article/details/107557214
  教程：https://www.cnblogs.com/TaoingBk/p/13755132.html
  下载：https://github.com/c0ny1/captcha-killer/tree/0.1.2
  需要配合图鉴、百度等打码平台的api（图鉴精度比较好）
  ```
  
---
**技巧**

- intruder 

  ```
  添加变量
  选择attack type 模式
  	sniper 狙击模式 ：单个变量，字典取一行，发一次请求
  	battering ram 散弹模式：多个变量，字典取一行，发一次
  	pitchfork 音叉模式：多个变量，每个位置一个字典，每个字典去一行，进行一次请求，请求数量由最少一个字典决定
  	cluster bomb 集束炸弹：多个变量（一般不超过3个），每个位置一个字典，进行组合请求
  选择字典 -可以传txt文件，可以粘贴
  option
  ```

  


---

**问题**

1.正常能访问，但使用burp拦包后，网站403不能访问资源

原因：网站使用http 2.0协议，不能拦截包

解决：使用HttpCanary监控网络包，然后修改内容进行重放（本质不会拦截网络包）

---

**插件**

```
ShiroScan：https://github.com/Daybr4ak/ShiroScan
fofa:https://github.com/0nise/burp-fofa
插件：https://github.com/Mr-xn/BurpSuite-collections
```

