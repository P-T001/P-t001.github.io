## 突破disable_functions

---

介绍：

```
phpinfo可以看到，主要是php.ini设置disable_functions禁止相关函数执行
```

绕过disable_functions的手法：(相关教程：https://www.freebuf.com/articles/web/192052.html)

```
1.攻击后端组件，寻找存在命令注入的、web 应用常用的后端组件，如，ImageMagick 的魔图漏洞、bash 的破壳漏洞
2.寻找未禁用的漏网函数，常见的执行命令的函数有 system()、exec()、shell_exec()、passthru()，偏僻的 popen()、proc_open()、pcntl_exec()，逐一尝试
3.mod_cgi 模式，尝试修改 .htaccess，调整请求访问路由，绕过 php.ini 中的任何限制
4.利用环境变量 LD_PRELOAD 劫持系统函数，让外部程序加载恶意 *.so，达到执行系统命令的效果
（使用蚁剑来生成so文件和php文件，再次连接该生成的php文件）
```

