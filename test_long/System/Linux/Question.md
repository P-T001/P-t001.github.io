# Linux  question

---

1.安装服务

```
net-tools            # 安装后关于网络的所有命令都能使用（ifconfig、netstat等）
ntfs-3g              # 安装后可挂载ntfs格式存储介质
```

2.网络配置

ubuntu ：/etc/network/interfaces

```
auto eth0
iface eth0 inet static       
address 192.168.3.90
gateway 192.168.3.1
netmask 255.255.255.0
```



centos：/etc/sysconfig/network-scripts/ifcfg-eth0  （ip a 看一下网卡名是否eth0）

```
    DEVICE=eth0
    TYPE=Ethernet
    ONBOOT=yes
    NM_CONTROLLED=yes
    BOOTPROTO=static
    IPADDR=192.168.106.101
    NETMASK=255.255.255.0
    GATEWAY=192.168.106.2
    DNS1=114.114.114.114
    DNS2=8.8.8.8
```



systemctl restart network  # 重启网络服务

dns配置文件 /etc/resolv.conf

