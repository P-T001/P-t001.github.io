# STEGA-隐写

---

图片思路：

1.图片属性，详细信息隐藏信息

2.更改数据类型进行隐藏（rar或者zuo改为jpg等）

3.在不影响图像视觉效果情况下修改像素数据,加入隐藏信息

4.利用隐写算法将数据隐写到图片,常用算法:F5/guesss/LSB







图片解题:

1.图片属性，详细信息隐藏信息

2.winhex或nodepad 进行搜索ctf/flag/key等字样

3.kali执行binwalk xxx.jpg查看图片是否包含多个其他文件,再使用foremost xxx.jpg 进行自动分离,如只检测一个压缩包文件修改后缀即可

4.使用StegSolve.jar对图像进行通道扫描,分析data Extract的red blue green,看是否为LSB隐写

5.kali执行F5-steganography,在java Extract运行:   java Extract 123456.jpg图片的绝对地址 -p 123456

6.kali使用outguess-master工具（需要安装），检测是否为guess算法隐写: outguess -r xxx.jpg(目标文件绝对路径) xxx.txt(信息存放的文本)

