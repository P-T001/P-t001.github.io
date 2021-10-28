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

3.kali不兼容秘钥算法

问题：

```
Key exchange failed.
No compatible key exchange method.
```

解决：

```
vi /etc/ssh/sshd_config
---末尾增加一行
KexAlgorithms curve25519-sha256@libssh.org,ecdh-sha2-nistp256,ecdh-sha2-nistp384,ecdh-sha2-nistp521,diffie-hellman-group-exchange-sha256,diffie-hellman-group14-sha1,diffie-hellman-group-exchange-sha1,diffie-hellman-group1-sha1
----
重启ssh服务即可
```

4.ubuntu 16 使用vi输入问题任意数据会变成ABCD

```
sudo apt-get remove vim-common  # vim-tiny
sudo apt-get install vim        # vim full
```

