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
-
代    理：proxies = {"http": "http://127.0.0.1:10809","https": "https://127.0.0.1:10809"}
-
postdata：data={'参数名':'值'}
-
证书路径：verify=False （忽略https证书）
-
cookies={}
如果cookie是"x1=xxxx; x2=yyyyy"这种类型,通过以下可以变成字典
cookie='x1=xxxx;x2=yyyyy'
cookie_dict_1 = {}
cookies_list = cookie.split('; ')
    for cookie in cookies_list:
        cookie_dict_1[cookie.split('=')[0]] = cookie.split('=')[1]

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
req.encoding=req.apparent_encoding #将当前编码变成网页请求回来的编码，解决中文乱码问题
```

问题：

1.InsecureRequestWarning: Unverified HTTPS request is being made to host 'xxx.com'. Adding certificate verification is strongly advised. See: https://urllib3.readthedocs.io/en/latest/advanced-usage.html#ssl-warnings
  warnings.warn(

解决：

```
from requests.packages.urllib3.exceptions import InsecureRequestWarning
requests.packages.urllib3.disable_warnings(InsecureRequestWarning)
```