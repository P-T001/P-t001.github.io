# php syntax

---

数据类型

```
数据类型：
	字符串 $x="xxx";   //                               使用.连接两字符串
	整型   $x=500;     //正数、负数、十六进制数、八进制数；使用加减乘除
	浮点型 $x=10.356;  //带小数部分的数字，或是指数形式    使用加减乘除
	布尔型 $x=true;    
	数组   $x=array("zhangsan",14,'study');   //数组合并使用array_merge($x,$y)，如果空数组合并数字数字，会重新按顺序编号
		  array(0=>zhangsan,1=>14,2=>study); //相当于上一条
		  $x=array("name"=>"zhangsan","age"=>14,"type"=>"study"); //数组的json形式
		  数组合并也可使用+来合并，但是两数组有相同键名，第二个数组的相同键名会忽略掉
		  使用array_merge合并非数组类型：
              $beginning = 'foo';
              $end = array(1 => 'bar');
              $result = array_merge((array)$beginning, (array)$end);
              print_r($result);
              输出：
                  Array
                  (
                  [0] => foo
                  [1] => bar
                  )
```

输出

```
echo，print，print_r，var_dump 的区别

1.echo
输出一个或者多个字符串。

2.print
和 echo 最主要的区别： print 仅支持一个参数，并总是返回 1。

3.print_r
打印关于变量的易于理解的信息,如果给出的是 string、integer 或 float，将打印变量值本身。如果给出的是 array，将会按照一定格式显示键和元素。object 与数组类似。 记住，print_r() 将把数组的指针移到最后边。使用 reset() 可让指针回到开始处。

4.var_dump
此函数显示关于一个或多个表达式的结构信息，包括表达式的类型与值。数组将递归展开值，通过缩进显示其结构。

5.var_dump 和 print_r 的区别
var_dump 返回表达式的类型与值而 print_r 仅返回结果，相比调试代码使用 var_dump 更便于阅读
```

类与方法：

```
class man
{
	public $name=''; //公共变量
	public function say($name) //公共方法
	{  
		$this->name=$name;//对象变量
		return 'my name is'.$this->name;
	}

}
$jack=new 类名();  //创建名为jack对象
echo $jack->say('jack'); //调用类方法
```

比较

```
== 只比较值、===比较值和类型
if(1=="1"){
	echo "相等";
}else{
	echo "不相等"
}
输出：相等（值相等）

if(1==="1"){
	echo "相等"
}else{
	echo "不相等"
}
输出：不相等（值相等，类型不相等）
```

常量

```
//定义常量，全局在整个脚本中使用，name是常量名/value是常量值/type默认为false大小写敏感
define ( string $name , mixed $value ,$type = false ] ) 
例：
	// 区分大小写的常量名
    define("GREETING", "欢迎访问 Runoob.com");
    echo GREETING;    // 输出 "欢迎访问 Runoob.com"
    echo '<br>';
    echo greeting;   // 输出 "greeting"
    ----
    // 不区分大小写的常量名
    define("GREETING", "欢迎访问 Runoob.com", true);
    echo greeting;  // 输出 "欢迎访问 Runoob.com"
```

默认函数

```
strlen("xxx")                     //输出长度,3
strpos("hello world",'world')    //查找目标字符串的位置,从0开始，输出：6
```

