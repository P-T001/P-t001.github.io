# python3 syntax

---

### **数据类型**

**字符串**

```
mystr='xxxxx'  # 定义字符串

mystr.find(字符串,开始行数,结束行数)  # 查询字符串，从左往右 ,没有会输出-1，有会出现第几位开始的字符串
mystr.index(字符串,开始行数,结束行数) # 查询字符串，左往右,没有会报错，有会出现第几位开始的字符串
rfind、rindex ：右往左查询，但是显示的是左往右的效果一样
mystr.partition(字符串) # 显示在整个变量中，第一个字符串 （字符串前，字符串，字符串后）
mystr.count(字符串) # 统计字符串出现的次数
mystr.replace(被替换，替换，左到右换次数)   # 次数不写，默认全换
mystr.split(分割符,分割次数) # 切割完后是列表，不输入参数，默认是全部切割不可见字符（空格 \t \n等等）
mystr.capitalize()     # 把变量的第一个字符大写
mystr.title()          # 把变量的每一个单词首字符大写
mystr.lower()          # 把变量所有的大写变小写
mystr.upper()          # 把变量所有的小写变大写
mystr.startswith(字符串) # 是否以字符串开头对，返回true，错，返回false
mystr.endswith(字符串)   # 是否以字符串结尾，对，返回true，错，返回false
mystr.ljust(宽度)        # 左对齐，宽度(长度)是x，用空格填充
mystr.rjust(宽度)        # 右对齐
mystr.center(宽度)       # 居中，填充宽度
mystr.lstrip()           # 删除变量左边的空白字符
mystr.rstrip()           # 删除变量右边的空白字符
mystr.strip()            # 删除变量左右两边的空白字符
mystr.splitlines         # 按照行分割，返回一个包含各行作为元素的列表
mystr.isalpha            # 如果变量里所有字符都是字母，返回true ，否则false
mystr.isdigit            # 如果变量里所有字符都是数字，返回true ，否则false
mystr.isalnum            # 如果变量里所有字符都是字母或数字，返回true ，否则false
mystr.isspace            # 如果变量里只有空格，返回true，否则false
```

**元组**（不可修改）

```
tup=(x1,x2)
选：
	tup[n]           # 选择第n位
其他:
	tup.count(x)     # 统计x出现的次数
	tup.index(x,n1,n2) # 查找字符串从n1开始到n2结束,出现的索引位
	...
```

**列表**

``` 
li=[x1,x2]  # 定义列表
增：
	li.append(x)     # 将x添加到列表末位
	li.extend(x)     # 将x的元素逐一加到列表末位
	li.insert(n，x)  # 将x插入到n位上
改：
	li[n]=xxx        # 将n位的元素改成xxx
删：
	del li[n]        # 将n位的元素删除
	li.pop(n)        # 默认删除列表末尾的元素，如果加参数，就是删除指定位
	li.remove(x)     # 删除指定的元素
排：
	li.sort()        # 将列表内元素从小到大排列，参数reverse = True则大到小排列
	li.reverse()     # 列表内元素顺序倒转
选：
	li[n]            # 选择第n位的元素
```

**字典（json格式）**

```
di={'name':'x1','age':'x2'}      # 定义字典 key:value
选：
	di.get(key,default=不存在返回值) # 输出key对应的value值
	list(di.keys())	                # 选择字典中所有key，并以列表方式存储
	list(di.values())               # 选择字典中所有values，并以列表方式存储
	list(di.items())                # 选择字典中所有key,value，并以列表嵌元组方式存储
增、改：
	di[key]=value 			       # key存在的会修改对应value，不存在则添加
删：
	del di[key]                     # 删除key和对应value
	del di                          # 删除字典
	di.clear()                      # 清空字典，变空字典
其他：
	len(di)                         # 统计字典长度
	...                      
```

**数据类型转换**

```
字符串->字典:
	eval(字符串)
	import json;json.loads(字符串)    # json格式字符串转换为字典
字符串->列表:
	list(字符串)                      # 字符串每个元素切割,输出成列表
	eval(字符串)                      # 将列表格式的字符串转换为列表格式
	字符串.split("切割符号")           # 切割符号,输出成列表
	import re;re.split("&|=",字符串)  # 正则&或=均切割,输出成列表
字符串->元组:
	tuple(字符串)
---
列表->字符串:
	str(列表)       # 列表符号也会变成字符串
	'拼接符'.join([str(i) for i in 列表])  # 列表元素拼接成字符串(列表元素必须字符串)
列表->字典:
	dict(列表)  # 列表格式[['key1','value1'],['key2','value2']]
	dict(zip(key列表,value列表))  # 两个列表长度一致,否则后面的无法显示
---
字典->字符串:
	str(字典)       # 字典符号也会变成字符串
	import json;json.dumps(字典)
字典->列表:
	list(字典.keys())  
	list(字典.values())
```

### **循环**

```
while循环：
while 条件： # 可以True 死循环，该条件是循环条件，满足则继续
	pass
	continue # 跳过本次循环，继续下一个循环
	break    # 跳出整个循环
---
for循环:(xxx是一个多元素集)
for i in xxx:
	pass
	
for高级写法：外面一定要有列表或者元素
[i for i in xxx if i == 0] # 循环每个xxx的元素i，如果i为0，则添加到列表中
	
```

### **判断**

```
if x == 0:    # 首先判断
	pass
elif y == 0:  # 二次判断
	pass
elif h != 0:  # 三次判断
	pass
else:         # 以上都不满足
	pass
```

### **尝试运行（异常处理）**

```
try:
	pass  # 功能代码
	raise RuntimeError(title)  # 主动抛出异常
except RuntimeError as R:
	print(R)   # 
except 错误类型: # Aexception as result：
	pass  # 根据错误类型，执行操作
except Exception as E: # 其他错误
	print(E)  #输出错误信息
else:   # 运行无异常才会执行
	pass
finally： # 无论是否异常都会执行
	pass
---
错误类型：
IndentationError：expected an indented block 
代码没有对齐

SyntaxError: invalid syntax
非法语句，语法错误

TypeError: 'int' object is not subscriptable
类型错误。输出的东西出错，维度错了；
没有维度的是字符串、数字；
一维就是列表、元组、字典；多维就是列表、元组、字典的嵌套；n维就代表嵌套n-1次，如lists[x] =1维

ValueError: not enough values to unpack (expected 3, got 2)
没有足够多的值，定义等于的是3个，但是实际只有2个值

NameError: name 'mc' is not defined
名字错误，前面没有定义mc这个变量

TypeError: unsupported operand type(s) for /: 'NoneType' and 'int'
类型错误，/除号前面的不是变量返回的不是数字

UnboundLocalError: local variable 'name' referenced before assignment
局部变量错误：循环前面没有name这个变量
```

### **自定义类与函数

```
自定义类：
# PS:
#   def __xx__():的是初始化方法（魔法方法属性）
#   类是模板不占内存空间，对象是根据类模板创建出来，占用内存空间
#   self是默认需要添加的，代表类自己本身
class xxx(object):  #object默认的父类，也可以导入其他模块的类名进行继承
	def __init__(self,参数1,参数2...): # 类创建成对象时的设置的参数
		self.参数1=参数1
		self.参数2=参数2
		...
	def __str__(self): # 输出对象时的操作
	def __add__(self): # 创建对象时的操作
	def __del__(self): # 删除对象时的操作
	...
	def xxx(self,xxx参数1,xxx参数2):     # 自定义的类方法
		pass
if __name__ == '__main__':   #判断是否本地调用，是才会执行下面
	x=xxx(参数1,参数2)        # 根据xxx类创建对象
	x.xxx(xxx参数1,xxx参数2)  # 调用该类方法
---
自定义函数：
def xxx(参数1,参数2):
	pass
```

### **导库（模块、文件）**

```
from xxx import *       # 导入xxx模块（文件）的全部类、函数，调用时直接以类名、函数名来调用
from xxx import xx as X # 导入xxx的xx类或方法，并取别名
from xxx import x1,x2   # 导入xxx的x1、x2
import xxx              # 导入xxx模块（文件）的全部类、函数，调用时需要“xxx.”加上类目、函数名来调用
```

