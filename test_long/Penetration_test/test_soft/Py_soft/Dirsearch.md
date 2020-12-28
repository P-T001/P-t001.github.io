# Dirsearch

---
github下载：
```
https://github.com/maurosoria/dirsearch
```

常用：

```
python dirsearch.py -u http://www.xxx.com/ -e * --proxy=http://127.0.0.1:10809 -x 500,403,400,401 --random-agents
```

参数：

```
-u  目标地址
-e  字典选择php、jsp、asp等后缀，不知道可以选择*
--proxy=http://x.x.x.x:xxx    代理设置
-x 不显示的状态码 
--random-agents  随机请求user-agents
```

