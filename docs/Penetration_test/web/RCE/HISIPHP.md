# HISIPHP

---

- 影响版本：2.0.10

- 来源：https://www.cnblogs.com/Rain99-/p/12240052.html

  后台插件导入get5he11

  ```
  1.下载应用
  在自己本地搭建后台/系统扩展/应用市场/安装开发助手 进行安装
  网站路径/runtime/app/xxx.zip
  2.构造应用
  解压后，在其中一个修改成webshell
  /upload/application/developer/admin/Module.php(模块列表)
  /upload/application/developer/admin/Plugins.php(插件列表)
  写入shell后重新压缩
  3.导入应用
  目标后台/系统扩展/本地模块/导入模块/上传模块安装包/含shell新压缩的包
  目标后台/系统扩展/本地模块/待安装/安装开发助手/启用
  4.进行访问
  开发助手/应用中心/模块列表 即我们传上去的shell
  开发助手/应用中心/插件列表 （如果是Plugins.php则访问插件列表）
  ```

  