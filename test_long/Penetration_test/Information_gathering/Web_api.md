# Web api

source: `{{ page.path }}`

---

手机号码归属和运营商

## 360 接口

```
https://cx.shouji.360.cn/phonearea.php?number=188xxxxxxx
return
{
  "code": 0,
  "data": {
    "province": "北京",
    "city": "",
    "sp": "联通"
  }
}
```

## ITEBLOG 接口

```
https://www.iteblog.com/api/mobile.php?mobile=188xxxxxxx

return

{
  "ID": "28088x",
  "prefix": "185191x",
  "province": "北京",
  "city": "北京",
  "operator": "中国联通",
  "areaCode": "010",
  "zip": "100000",
  "ret": 0,
  "searchStr": "188xxxxxxx",
  "from": "https://www.iteblog.com/api/mobile.php",
  "ip": "114.243.220.x",
  "ua": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/62.0.3202.94 Safari/537.36"
}
```





---