# Requests

---

安装：pip install requests  |导入：import requests

请求方式：

```
get请求 ：requests.get(url,headers,proxies)       |url:目标地址、headers：请求头部、proxies：代理
post请求：requests.post(url,headers,proxies,data) |url:目标地址、headers：请求头部、proxies：代理、data：postdata
head请求：requests.head(url,headers,proxies)      |url:目标地址、headers：请求头部、proxies：代理
```

请求参数：

```
请求头部：headers = {'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/84.0.4147.105 Safari/537.36', 'content-type': 'charset=utf8'} 
代    理：proxies = {"http": "http://127.0.0.1:10809","https": "https://127.0.0.1:10809"}
postdata：data={'参数名':'值'}
```

保持会话：

```
res_S=requests.Session()                                 # 创建会话对象
res_S.headers.update(self.header)                        # 更新header
res_S.proxies.update(self.proxies)                       # 更新proxies
res_S.get(url) |res_S.post(url,data=)
```

获取返回内容：

```
如：req=requests.get(url)
req.status_code     # 返回状态码|int
req.text            # 请求网页的文本
```

