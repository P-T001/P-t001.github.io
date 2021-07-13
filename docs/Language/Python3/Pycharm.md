# Pycharm

---

1、整理request里的header变成json格式

```
将header复制到pycharm里单独放在一个文件
使用ctrl+r 快速替换，勾选Regex
替换源为：(.*):\s(.*)$
替换为："$1": "$2",
点击Replace all #替换全部
然后ctrl+alt+L 整理格式
```

2、将pycharm中sql语句标黄的去掉

```
在Settings=>Editor=>Language Injections中将:
python: "SQL select/delete/insert/update/create"的勾选给去掉就OK
```

