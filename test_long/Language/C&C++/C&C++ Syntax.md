# C&C++ Syntax

---

## **介绍**

```
C和C++使用不同编译方式，使用同一个编译器
C&C++部分代码可以相互兼容
```

## **文件头**

```
//C使用.h和c开头的头文件，c++使用无.h头文件（名字空间均为std）|包含头文件，可调用里面的类、函数等
//默认头：
#include <deque>　　　　　   //STL 双端队列容器
#include <exception>　　　  //异常处理类
#include <fstream>　　　    //文件输入／输出
#include <functional>　　　 //STL 定义运算函数（代替运算符）
#include <limits>　　　　   //定义各种数据类型最值常量
#include <list>　　　　　　 //STL 线性列表容器
#include <map>　　　　　　  //STL 映射容器
#include <iomanip>　　　    //参数化输入／输出
#include <ios>　　　　　　  //基本输入／输出支持
#include <sstream>　　　　 //基于字符串的流
#include <stack>　　　　　 //STL 堆栈容器
#include <algorithm>　　　 //STL 通用算法
#include <bitset>　　　　　//STL 位集容器
#include <cctype>　　　　  //字符处理
#include <stdexcept>　　　 //标准异常类
#include <streambuf>　　　 //底层输入／输出支持
#include <string>　　　　　//字符串类
#include <utility>　　　　 //STL 通用模板类
#include <vector>　　　　　//STL 动态数组容器
#include <iosfwd>　　　　　//输入／输出系统使用的前置声明
#include <cerrno>　　　　 //定义错误码
#include <clocale>　　　　//定义本地化函数
#include <cmath>　　　　　//定义数学函数
#include <complex>　　　　 //复数类
#include <cstdio>　　　　 //定义输入／输出函数
#include <cstdlib>　　　　//定义杂项函数及内存分配函数
#include <cstring>　　　　//字符串处理
#include <ctime>　　　　　//定义关于时间的函数
#include <iostream>　　　 //数据流输入／输出
#include <istream>　　　　 //基本输入流
#include <ostream>　　　　 //基本输出流
#include <queue>　　　　　 //STL 队列容器
#include <set>　　　　　　 //STL 集合容器
#include <cwchar> //宽字符处理及输入／输出
#include <cwctype>　　　　 //宽字符分类
#include <complex.h>　　 //复数处理
#include <fenv.h>　　　　//浮点环境
#include <inttypes.h>　　//整数格式转换
#include <stdbool.h>　　 //布尔环境
#include <stdint.h>　　　//整型环境
#include <tgmath.h>　　　//通用类型数学宏
```

## **名字空间**

```
//名字空间C++特有
//定义名字空间，空间里可以定义类、函数等
namespace Zhangsan{
	FILE fp = NULL;
}
namespace Lisi{
	FILE fp = NULL;
}
int main(){
	using namespace Lisi;               //默认使用Li名字空间（包括所有的类、函数等）
	//using Lisi::fp;                   //默认使用Li名字空间的fp
	fp=fopen('x.txt','r');              //使用的是默认Lisi的fp
	Zhangsan::xx=fopen('x.txt','r')     //使用的是Zhangsan的fp
}
```

## **C结构体与C++类**

```
//C中用结构体、函数等，面向过程:
#include <stdio.h>  //C语言输入输出头文件
struct Student{     //定义结构体
	//结构体只能定义变量，格式：数据类型 变量名;
	char *name;   
	int age;
	...
};
//定义函数
void display(struct Student stu){
	printf('name:');
	scanf('%s',&stu.name); //输入name
	printf('age:');
	scanf('%d',&stu.age);  //输入age
	printf("%s,%d",stu.name,stu.age) //输出name和age
}

//主程序
int main(){
	struct Student stu1; //创建对象
	stul.name='xx';     //定义结构体变量name
	stul.age=16;        //定义结构体变量age
	display(stul);      //将结构体对象丢到函数运行
	return 0;           //返回正确
}
---
//C++用名字空间、类、函数等，面向对象:
#include <iostream> //c++的输入输出头文件，C++也可以用c的头，但函数不一样
using namespace std; //声明默认使用std（来自头文件）名字空间的函数，PS：最好在局部中（类、函数等）使用，不然容易和其他命名冲突，本次是为了方便才在全局使用。
class Student{   //定义类
public:
	//成员变量
	char name;   //定义类的变量name
	int age;     //定义类的变量age
	//成员函数
	void display(){
		cin>>name>>age; //输入两次，第一次给name，第二次给age
		cout<<"name:"<<name<<",age:"<<age<<endl;
	}
}
//主程序
int main(){
	class Student stu1;  //创建对象
	stu1.name='xxx';     //定义对象变量name
	stul.age=16;         //定义对象变量age
	stul.display(stul);  //将对象丢到类方法运行
	return 0;
}

```

## **循环**

```
int num=0;
for(ini i=1;i<=n;i++){        //数据类型 起始条件;终止条件;每次循环i+1
	num+=i                    //每次循环操作
}
```

## **申请和释放内存**

```
C:
int *p = (int*) malloc( sizeof(int) * 10 );  //分配10个int型的内存空间
free(p);  //释放内存

C++:
int *p=new int;  //分配1个int的内存，会根据数据类型自动分配
delete p;        //释放内存

int *p=new int[10];  //分配10个int的内存，会根据数据类型自动分配
delete[] p;        //释放p内存，原本是多少个默认删除多少个
```

函数

```
//定义函数，参数默认值（有参数默认值的后面参数都必须要有参数默认值）
void func(int a,int b=10){
	int c=0;
	c=a+b;
}
//函数重载：同名函数,参数列表不同（个数、数据类型、排列顺序等）
void Swap(char *a,char *b){
	char temp=*a;
	*a=*b;
	*b=temp;
}
void Swap(int *a,int *b){
	int temp=*a;
	*a=*b;
	*b=temp;
}
```

