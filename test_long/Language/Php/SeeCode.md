# SeeCode

---

- 辅助工具

 ```
 rips
 seay代码审计系统
 ```

- 全局搜索（看是否可控、是否无过滤）

 ```
输入变量：
    $_POST     # post请求
    $_GET      # get请求
    $_REQUEST  # post请求+get请求
    $_COOKIES  # 获取cookie值
    $_SERVER['REMOTE_ADDR']   # 获取客户端的REMOTE_ADDR
    getenv()    # 获取请求header的参数值如：HTTP_FORWARDED、
    
    
写文件：
$open=fopen('文件路径+文件名','模式a/w');          # 创建文本对象
fwrite($open,'内容');   # 写入操作
fclose($open);          # 关闭文本

file_put_contents('文件路径+文件名','文件内容','模式a/w'); # 写入文件

文件包含：
require_once();        # 包含一次
include_once();        # 包含一次
require();
include();

任意文件下载：
download 、fileName 、filePath、write、getFile、getWriter

文件上传：
Upload、write、fileName 、filePath

sql注入：
Select、Dao 、from 、delete 、update、insert

密码：
PASSWORD、密码
 ```

  过滤函数

```
addslashes  # 会对符号进行转义
```

