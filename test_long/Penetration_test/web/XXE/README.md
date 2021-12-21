# XXE

---

**XXE-外部实体注入**

- 介绍

  ```
  XXE是XML外部实体（XML External Entity）注入的简称，在OWASP TOP 10 2017版中位居A4，属于严重级别的漏洞。此攻击可能导致任意文件读取，远程代码执行，拒绝服务，服务器端请求伪造，内网端口探测，以及其他系统影响。
  ```

- XML和DTD基础

     XML是可扩展性标记语言，类似HTML的标记语言，但标签是自定义的。DTD是文档类型定义，用来为XML文档定义语义约束，可以在xml文件中声明，也可以在外部引用

     XML文件结构:

     ```
<? xml version="1.0" encoding="utf-8"?>
DTD部分（可选）
<root>Test</root>
     ```

- DTO引用和实体声明

  DTD内部声明：<!DOCTYPE 根元素 [实体声明]>
  DTD外部引用：<!DOCTYPE 根元素名称 SYSTEM “外部DTD的URL">
  DTD内部实体声明：<!ENTITY 实体名称 “实体的值">
  DTD外部实体声明：<!ENTITY 实体名称 SYSTEM “URI/URL">

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <!DOCTYPE root [
  <!ENTITY name "XXE test">]>
  <root>&name;</root>
  ```

- 漏洞成因

  ```
  1、没有过滤用户提交的XML数据
  2、使用的开发语言可以解析xml外部实体，如php环境中libxml库≤2.9.0默认启用了外部实体
  ```
- 漏洞常见位置
  
  ```
  1、涉及到提交xml数据的功能处
  2、xml文件上传处
  3、office文档上传预览处
  4、某些json格式传递数据的地方，可以修改其Content-Type为application/xml，并尝试进行XXE注入
  ```

- 支持协议

  ```
  libxml2 : file/http/ftp
  PHP     : file/http/ftp/php/compress.zlib/compress.bzip2/data/glob/phar
  
  ```

  