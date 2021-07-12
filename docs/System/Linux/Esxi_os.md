# Esxi_os

---

介绍：

```
可以做集群（将几台服务器的资源通过一个数据中心虚拟机进行管理）
版本6.0之前有client管理,之后只能web管理
```

绕密码：

```
centos 6.6 bin版的linux镜像做成PE启动盘
F12 select *
使用USB s*  启动U盘
读秒时，按任意键，选择系统
选择rescue
https://m.linuxidc.com/Linux/2015-03/114942.htm
救援模式选择hard * 选择最后sdb1

进入后
df -h  
fdisk -l   # 查看有多少个盘和分区，可能只有原来的sda1  但是却存在sda5 
原因是分区表没读到
mount /dev/sda5  /mnt/sda5
cp /mnt/sda5/state.tgz /tmp
cd /tmp/
tar xzvf state.tgz
tar xzvf local.tgz
vi /tmp/etc/shadow
修改root的密码
root:空:*   (即可)
rm -rf state.tgz local.tgz
tar  czvf  local.tgz etc
tar  czvf  state.tgz local.tgz 
cp state.tgz /mnt/sda5
reboot  #重启

进去后直接空密码登陆

计算机可通过与esxi同版本的客户端进行连接
```

