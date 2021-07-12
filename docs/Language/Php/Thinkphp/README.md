# Thinkphp

---

目录：

{% include list.liquid all=true %}

---

Thinkphp3/Thinkphp5

Thinkphp3开发手册：http://document.thinkphp.cn/manual_3_2.html#auto_build

```
目录结构：
www
|——index.php  入口文件
|——application 应用目录，里面放多个app，也可以不要这个应用目录在外面建app的目录
|——public     资源文件
|——ThinkPHP   框架系统目录，全局函数、设置等
│  ├─Common       核心公共函数目录
│  ├─Conf         核心配置目录 
│  ├─Lang         核心语言包目录
│  ├─Library      框架类库目录
│  │  ├─Think     核心Think类库包目录
│  │  ├─Behavior  行为类库目录
│  │  ├─Org       Org类库包目录
│  │  ├─Vendor    第三方类库目录
│  │  ├─ ...      更多类库目录
│  ├─Mode         框架应用模式目录
│  ├─Tpl          系统模板目录
│  ├─LICENSE.txt  框架授权协议文件
│  ├─logo.png     框架LOGO文件
│  ├─README.txt   框架README文件
│  └─ThinkPHP.php    框架入口文件
优先级：app应用配置>ThinkPHP全局配置
app目录：
|——Common         公告模块
|——Home           默认模块
│  ├─Conf         模块配置文件目录
│  ├─Common       模块函数公共目录
│  ├─Controller   模块控制器目录，具体实现功能方法
│  ├─Model        模块模型目录，数据模型定义
│  ├─View         模块视图文件目录，前端展示页面
|——xxxxx          自定义模块，如admin，和Home结构一样
|——Lib         
|——Runtime        缓存目录
│  ├─Cache        模板缓存目录
│  ├─Data         数据目录
│  ├─Logs         日志目录
│  ├─Temp         缓存目录

```

Url访问：

```
http://xxxx/index.php/模块/控制器名/操作/参数名/参数值
```

模块设计：

```
Application      默认应用目录（可以设置）
├─Common         公共模块（不能直接访问）
├─Home           前台模块
├─Admin          后台模块
├─...            其他更多模块
├─Runtime        默认运行时目录（可以设置）
```

