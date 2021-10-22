# shell syntax

---

- 语法

  ```
  调用变量时：$name -> ${name} 更好的让编译器去辨认变量，
  数据类型：
  	数组名=("","","") # 调用：${数组名[下标]}，定义：数组名[下标]=值，调用所有${数组名[@]}
  	
  数据类型转换：
  	数字->字符串：
          num=$((1=1))
          echo ${num}""  # 将数字和空字符串拼接变成字符串
  	
  变量定义：
  	num=$(ps -ef | grep http | grep -v grep | wc -l)  # 将命令结果定义变量，调用时$num
  	read -p "input your name and age" name age   # 调用时$name $age
  	read -p "input your name"  # 没有定义时，调用时$REPLY
  	read -s -p "input your password" password # 隐藏方式读取
  	l
  	
  运行传参：
  	$0：表示运行sh脚本名
  	$n：表示运行sh脚本时的第n个参数,从1开始
  	$#：传递给脚本或函数的参数个数
  	$*：传递给脚本或函数的所有参数。当被双引号""包含时，会将所有的参数从整体上看做一份数据，而不是把每个参数都看做一份数据。
  	$@：传递给脚本或函数的所有参数。当被双引号""包含时，仍然将每个参数都看作一份数据，彼此之间是独立的
  	$?：上个命令的退出状态，或函数的返回值
  	$$：当前Shell的进程ID。对于Shell脚本，就是这些脚本所在的进程ID
  	
  预设输入：
      read -n1 -p "Do you want to continue [Y/N]" answer # -n1 表示只读取输入的1行
      case $answer in 
      Y|y) echo
      	echo "continue";;
      N|n) echo
      	echo "exit";;
      	exit
      esac
  	
  文件读取：
  	count=1
  	cat test.txt|while read line
  	do
  		echo "line $count;$line" # 输出行数和对应行内容
  		count= $[$count+1]  # 行数累加
  	done
  	
  ```

-  判断

  ```
  if [command];then
  	echo "1"
  elif [command];then  # 多条件and ：elif [command]&&[command];then
  	echo "2"
  else
  	exit 
  fi
  
  [command]:
  	[ -d "Dir" ]  # 如果目录存在则为真 , [ ! -d "Dir"] # 如果目录不存在则为真
  	[ -f "FILE" ] # 如果文件存在则为真 , [ ! -f "FILE"] # 如果文件不存在则为真
  	[ "字符串1" = "字符串2" ] # 如果字符串1=字符串则为真，!= 则为非
  	[ -z "字符串" ] # 如果字符串长度为零则为真
	[ -n "字符串" ] # 如果字符串长度为非零则为真
  	[ int1 OP int2 ] # int1和int2都是整数，OP：-eq等于，-ne不等于，-lt小于，-le小于等于，-gt大于，-ge大于等于，比较大小使用
  	[ -r "File" ] # 如果文件存在并有可读权限为真
  	[ -w "File" ] # 如果文件存在并有可写权限为真
  	[ -x "File" ] # 如果文件存在并有可执行权限为真
  
  ```
  
- 循环

  ```
  for 循环
      for a in {1..10}  #$(seq 1 10) #也是1-10整数的意思
      do   # 开始循环
          执行命令
      done # 结束循环
  
  while循环：	
      while 条件    # 条件为真，可以是((i<=10))或者 read 文件，非空则跳出循环
      do
  		执行命令
      done
      
  until循环：
  	until 条件    # 条件为假进入循环
  	do
  		执行命令
  	done
  		
  ```

- 函数定义

  ```
  function 函数名(){
  	local a=1 # 局部变量 ，局部变量>全局变量
  }
  ```

  