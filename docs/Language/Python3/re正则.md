# re正则

---

匹配模式：

```
re.I 忽略大小写
re.L 表示特殊字符集 \w, \W, \b, \B, \s, \S 依赖于当前环境
re.M 多行模式
re.S 即为 . 并且包括换行符在内的任意字符（. 不包括换行符），在html中选择需要加
re.U 表示特殊字符集 \w, \W, \b, \B, \d, \D, \s, \S 依赖于 Unicode 字符属性数据库
re.X 为了增加可读性，忽略空格和 # 后面的注释
多个模式表示例：re.I|re.L
匹配模式可以为空
```

正则提取符号条件的所有字符串

```
re.findall(正则表达式,目标字符串,匹配模式)
例：
    ss='<img src="/x.jpg"><a href="/x.php">'
    result=re.findall('(src=|href=).*?((http://|https://|/).*?(\.jpg|\.php).*?)"',ss,re.I)
    for i in result:
    	print(i[0]) # src=  href=
    	...
    	print(i)    # ('src=', '/x.jpg', '/', '.jpg') ('href=', '/x.php', '/', '.php')
注释：
    .*?  表示所有
    ()   表示需要获取的内容，如果有多个就均获取变成元组
    (src=|href=) 表示获取src=或href=
    \.jpg  因.在正则内代表一个字符串，这里需要\来转义
    findall 获取输出的数据为列表，每个()对应列表中的元组，与finditer区别在于不能获取整个正则匹配的数据
    
re.finditer(正则表达式,目标字符串,匹配模式)
例：
	ss='<img src="/x.jpg"><a href="/x.php">'
	result=re.finditer('(src=|href=).*?((http://|https://|/).*?(\.jpg|\.php).*?)"',ss,re.I)
	for i in result:
		print(i.group())  # src="/x.jpg"  href="/x.php"
		print(i.group(1)) # src=  href=
		....
		print(i.groups()) # ('src=', '/x.jpg', '/', '.jpg') ('href=', '/x.php', '/', '.php')
注释：
	finditer 获取的result是对象，循环每个的group就是整个正则匹配的数据，如果需要单独某个()内容需要加数字如：i.group(1)
```

正则提取符号条件的第一个字符串

```
re.search(正则表达式,目标字符串,匹配模式)
匹配整个字符串，直到找到一个匹配的，否则返回none
例：
	ss="Cats are smarter than dogs"
	result=re.search( r'(.*) are (.*?) .*', line, re.M|re.I)
	for i in result:
		print(i.group())  # Cats are smarter than dogs
		print(i.group(1)) # Cats
		print(i.group(2)) # smarter
		print(i.groups()) # ('Cats','smarter')
	
re.match(正则表达式,目标字符串,匹配模式)
只匹配字符串开始，如果字符串开始不匹配，则失败返回none
例：
	ss="Cats are smarter than dogs"
	result=re.match( r'(.*) are (.*?) .*', line, re.M|re.I)
	for i in result:
		print(i.group())  # Cats are smarter than dogs
		print(i.group(1)) # Cats
		print(i.group(2)) # smarter
		print(i.groups()) # ('Cats','smarter')
```

常用正则

```
邮箱：.*?([0-9a-zA-Z_\.-]{1,35}@[0-9a-zA-Z-_]{1,15}\.([a-z]{1,3}).*?
注释：[0-9] 0到9范围 [a-z] a到z范围 [_\.-] 单个_ . - 因.是有功能的字符串需要转义
      {1,35} 代表前面字符串有1-35个占位  ()代表取值里面内容
```

