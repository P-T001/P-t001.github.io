#  Backdoor search

---

**教程**

```
https://www.freebuf.com/column/162604.html
https://kionf.com/2018/10/25/rookit-vlany/   # vlany具体操作
https://www.freebuf.com/articles/system/223311.html
下载：
https://github.com/mempodippy/vlany
https://github.com/mempodippy/cub3 
PS:
vlany无法在 CentOS 6.6 以上的任何系统上正确安装。(依赖的cub3也是如此)
```

**LD_PRELOAD 劫持**

  ```
  介绍：
  	LD_PRELOAD是环境变量，根据linux预加载机智，相应系统命令会加载到LD_PRELOAD环境变量中。
  劫持方式：
  	LD_PRELOAD=/lib/xxx.so # 将环境变量设置为预加载的恶意动态链接库
  	export LD_PRELOAD      # 导出环境变量
  检测方式：
      echo $LD_PRELOAD  #能看到恶意加载的库文件路径
      strace -f -e trace=file /bin/ls
      能看到open了恶意库文件.so 来劫持ld.so.preload
          open("/lib/xxx.so")
          access("/etc/ld.so.preload")    # 劫持之后这个文件无法被cat查看
  ```

**ld.so.preload劫持（目前主流）**

  ```
  目标文件：/etc/ld.so.preload 动态连接器
  劫持方式：
  	https://github.com/mempodippy/cub3   # 无后门版
  检测方式：
      cat /etc/ld.so.preload
      busybox cat /etc/ld.so.preload  #显示/lib/xxx.so 恶意动态链接库路径
      busybox string /lib/xxx.so   # 查看该文件
  	strace -f -e trace=file /bin/cat  # 调试跟踪cat命令
  	能看到劫持ld.so.preload和打开了恶意动态链接库
  		access("/etc/ld.so.preload") 
  		open("/etc/ld.so.preload")
  		open("/lib/xxx.so")
  处理方式：
  	./busybox lsattr /etc/ld.so.preload      # 查看该文件的属性 ---ia----隐藏属性
  	./busybox chattr -ia /etc/ld.so.preload  # 解除隐藏属性
  	rm -rf /etc/ld.so.preload     # 删除
  	rm -rf /lib/xxx.so
  	
   
  ```

**修改动态连接器劫持**

    ```
    目标文件：/etc/ld.so.preload 调用修改成其他
    劫持方式：
        https://github.com/mempodippy/vlany  # 设置后门版
    检测方式：
        strace -f -e trace=file /bin/ls
        安装完相应的恶意程序以后，其默认库文件被修改为/bin/.Kv8Xqykz
        access("/bin/.xxxxxx")
    处理方式：(输入任意内容到ld.so.preload，然后删除)
        cat /etc/ld.so.preload
        echo /lib/test.so > /etc/ld.so.preload
        rm -f /etc/ld.so.preload
    
    ```



---

**RedXOR**

- 介绍背景

  ```
  是一个针对Linux终端和服务器的新的复杂后门程序
  在2021年2月24号首次在VT(VirusTotal)上被上传以及发现
  ```
- 解决
  ```
  户根目录下存在".po1kitd.thumb"的目录，则该主机可能已经被控制了。受害者可以通过杀死来自“.po1kitd-update-k”二进制文件的进程，删除".po1kitd.thumb"和"/var/tmp/.po1kitd-k3i86dfv"目录，以及检查“/etc/init.d/”和"/usr/syno/etc/rc.d/“目录中是否存在名为“po1kitd-update.sh”的文件，若有则删除。还要将已经加载的Adore-ng rootkit从内核中卸载下来。最后还要查看系统日志，查看“.po1kitd-update-k”程序是否有在其他地方创建文件或目录，及时清除，确保擦除所有痕迹。
  ```
  