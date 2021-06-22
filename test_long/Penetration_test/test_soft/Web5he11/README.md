# Web5he11

---

目录：

{% include list.liquid all=true %}

---

### web5he11收集

```
https://github.com/johnjce/herramientas/tree/master/
https://github.com/weepsafe/phpshell
```

导致webshell不能执行命令的原因：（执行命令回显：red=127）

````
1.php.ini 中用 disable_functions 指示器禁用了 system()、exec() 等等这类命令执行的相关函数
2.web 进程运行在 rbash 这类受限 shell 环境中
3.WAF 拦劫
若是一则无法执行任何命令，若是二、三则可以执行少量命令
可以查看phpinfo查看
````

