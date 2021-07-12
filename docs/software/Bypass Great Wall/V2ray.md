# V2ray

---

来源：https://www.noobyy.com/

**服务端的搭建**

```
安装V2：
    bash <(curl -s -L https://git.io/v2ray.sh)
    1 #安装
    回车  #默认TCP
    端口号  #V2的端口号
    回车   #不启用广告拦截
    Y     #是否配置SS ，游戏加速需要用到
    端口号  #SS的端口号，不能与V2重复
    密码    #SS的连接密码
    回车    #选择SS加密协议，推荐默认
    疯狂回车即可安装完成，完成后会输出配置信息

开启BBR加速：（来源：https://teddysun.coms）
	wget --no-check-certificate https://github.com/teddysun/across/raw/master/bbr.sh && chmod +x bbr.sh && ./bbr.sh

问题：
1.配置成功后连不上，可能是因为防火墙的原因
	systemctl stop firewalld  
2.如要配置ss
inbounds加入
    {
      "port": 10087, // SS 协议服务端监听端口
      "protocol": "shadowsocks",
      "settings": {
        "method": "aes-128-gcm", // 加密方式
        "password": "yuan.ga" //密码
      }
    }

systemctl restart v2ray  #重启v2ray服务

3.配置文件路径：vi /etc/v2ray/config.json
```

**客户端下载**

- https://github.com/2dust/v2rayN/releases

