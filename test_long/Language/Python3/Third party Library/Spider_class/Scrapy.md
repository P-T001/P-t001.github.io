# Scrapy

---

## 安装篇

安装

```
pip install scrapy
```

windows安装如果出现错误信息：可能是没安装好twisted，需自行安装：

```
Twisted：为 Python 提供的基于事件驱动的网络引擎包。
Twisted下载链接：http://www.lfd.uci.edu/~gohlke/pythonlibs/#twisted
选择Twisted-18.9.0-cp36-cp36m-win_amd64.whl #36代表的是python3.6
pip install Twisted-18.9.0-cp36-cp36m-win_amd64.whl  
然后再次安装scrapy
pip install scrapy 
```

原理图：

![Photo_GPS-1.png](https://p-t001.github.io/image/blog/Scrapy-1.png)

---

## 实践篇

### 创建项目

```
scrapy startproject 项目名   #创建项目文件
cd  项目名                   #切换路径到项目里面，再创建爬虫应用
scrapy genspider app名 域名  #创建爬虫应用（每个爬虫应用都是在spider目录里面）
```

---

### 命令

```
scrapy genspder -l                #查看所有命令
scrapy genspider -d 模板名称       #查看模板
scrapy list                       #展示爬虫应用列表
scrapy crawl   爬虫应用名称        #运行单独爬虫应用  ，默认有日志，--nolog 取###消日志
scrapy fetch                      #测试网页
scrapy check                      #检查爬虫语法
```

---

### 目录结构

```
project_name/
   |--scrapy.cfg  #项目的主配置信息。（真正爬虫相关的配置信息在settings.py文件中）
   |--project_name/
       |-- __init__.py
       |--items.py   #设置数据存储模板，用于结构化数据，如：Django的Model
       |--middlewares.py  #下载器中间件
       |--pipelines.py  #数据处理行为，如：一般结构化的数据持久化
       |--settings.py  #配置文件，如：递归的层数、并发数，延迟下载等
       |--spiders/      #爬虫目录，如：创建文件，编写爬虫规则
      	   |--__init__.py
      	   |--__pycache__
      	   |--爬虫1.py  #爬虫应用
      	   |--爬虫2.py
      	   |--爬虫3.py
   |--main.py    #自行创建，
```

---

### settings.py（项目配置文件）

```
ROBOTSTXT_OBEY =False #默认是True ,验证目标robots.txt文件是否允许爬取
COOKIES_ENABLED = False  #默认ture，清除cookie，如需要自定cookie需要设置为False
DEFAULT_REQUEST_HEADERS  #cookie内容

设置状态码为以下时，重新15次请求:
RETRY_HTTP_CODES=[500,502,503,504,403,408,429] 
RETRY_TIMES=15
```

---

### main.py（项目运行文件）直接运行即可

```
from scrapy.cmdline import execute
execute('scrapy crawl 爬虫应用名 -o csv/result.csv'.split()) 
# 相当于cmd运行 （如果不想输出日志信息： --nolog） |-o csv/result.csv 导出到csv/result.csv
# scrapy crawl Game
```

