# github_syntax

---

常用：

```
搜索内容关键字 NOT 排除内容关键字  //排除内容关键字进行搜索，如果关键字有空格需要加引号
language:c++                    //搜索语言仓库为c++，-language:c++ 为排除该语言
user:xxxx                       //搜索用户为xxxx的仓库
pushed:>2019-01-01              //搜索更新时间大于2019-01-01 的仓库
stars:>10000                    //搜索stars大于10000的仓库
size:>1000                      //搜索文件大于1000kb的文件，如system size:>1000为含system的文件大于1000KB
path:/docs/                     //搜索路径出现/docs/的文件
```

组合常用

```
/路径/文件名.php
filename:文件名  path:/路径/  language:php
filename:文件名  path:/路径/,/路径2/  language:php  //满足两个路径的php仓库的文件名
```

