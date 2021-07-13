# Mirroring

---

## Raw

raw是原始的磁盘镜像格式，阿里云镜像一般是raw

system代表该服务器的系统盘，data代表该服务器的数据盘，如果只有system说明该服务器系统盘和数据盘放一起

无论是挂载还是转换，最好是对副本镜像进行操作

1.挂载方式

linux和windows的镜像都可挂载读取

```
在linux中挂载：
losetup -f                                # 查看设备空闲
losetup /dev/loop0 xx.raw                 # 挂载镜像到设备
kpartx -av /dev/loop0                     # 添加设备
mount /dev/mapper/loop0p1 /media/xxxx     # 挂载到该路径,该路径需要先创建
```

```
在linux中卸载：
umount /media/xxxx
kpartx -dv /dev/loop0
losetup -d /dev/loop0                     
```

2.转换方式

PS:转换时间较长，在linux和windows均可

```
qemu-img支持20多种格式转换：（qemu-img  -h   #获取帮助信息查看）
blkdebug、blkverify、bochs、cloop、cow、tftp、ftps、ftp、https、http、dmg、nbd、parallels、qcow、qcow2、qed、host_cdrom、host_floppy、host_device、file、raw、sheepdog、vdi、vmdk、vpc、vvfat
```

```
qemu-img convert -p -f raw xxx.raw  -O vmdk xxx.vmdk
参数：
-p 显示进度
-f 目标格式  转换前的文件路径
-O 转换格式  转换后的文件路径
```

使用vmware创建虚拟机，使用该vmdk即可（system、data）

```
qemu-img
https://cloudbase.it/downloads/qemu-img-win-x64-2_3_0.zip  #下载软件地址
https://github.com/cloudbase/qemu                          #源码地址
```

修改镜像密码：

linux系统挂载system标识得vmdk即可，在linux系统中将本地的/etc/shadow文件的root密码复制到镜像的/etc/shadow文件root用户中

PS：（记得备份原有镜像root，防止后期出现问题）

关闭linux系统或者卸载那个vmdk，启动镜像的vmdk虚拟机



如果条件可以，服务器搭建proxmox，可以直接读取raw等镜像格式运行

```
https://www.proxmox.com/en/downloads      #下载包
https://blog.51cto.com/6222666/2161799    #教程
```

