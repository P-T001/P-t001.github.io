# Masscan

---

-  在Debian/Ubuntu系统中安装方法如下

```
# sudo apt-get install git gcc make libpcap*
# git clone  https://github.com/robertdavidgraham/masscan
# cd masscan
# make
# cp masscan/bin/masscan /bin

```

  使用

```
./masscan -p80,8000-8100 10.0.0.0/8 --max-rate 100000
```



- Windows下安装请参考

```
https://www.4hou.com/penetration/6173.html
https://github.com/robertdavidgraham/masscan/
```

 使用

```
masscan.exe -p80,8000-8100 10.0.0.0/8 --rate=10000
-p 指定端口，可以1-20,21,22
--banners 获取banner值
-oJ xxx.json 输出结果为json格式
-oX xxx.xml  输出结果为xml格式
-iL 指定扫描文件中ip地址，ip地址可以是网段形式
--rate   每秒发包数
--banners  获取服务的特征信息banners
-e 网卡名   指定网卡发包
```





