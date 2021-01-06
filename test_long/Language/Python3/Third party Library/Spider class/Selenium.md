# Selenium

---

安装

```
pip install selenium   #不同系统模块不一样|MAC：seleniumMac
```

支持webdriver（浏览器驱动）

```
chrome、firefox、PhantomJS、IE、safari、opera
```

webdriver下载：（需要与你安装的浏览器版本对应）

```
chrome：https://chromedriver.storage.googleapis.com/index.html?path=2.29/
firefox：https://github.com/mozilla/geckodriver/releases
...
```

以chrome为例

环境准备

```
chromedriver.exe驱动需要放在浏览器安装目录：（如果没有这一步，需要在代码调用时定义驱动位置）
C:\Program Files (x86)\Google\Chrome\Application下，并将该路径加入环境变量
```

使用

```
from selenium import webdriver           # 导入模块
options=webdriver.ChromeOptions()
options.add_argument('cookie路径') # 填入浏览器保存cookie的路径，即使用爬虫访问的cookie路径都保存在这里
options.add_experimental_option('excludeSwitches',['ignore-certificate-errors'])   # 访问https时忽略报错
driver = webdriver.Chrome(executable_path="C:/chromedriver.exe",options=options)   # 创建chrome对象



driver.maximize_window()  #浏览器最大化
driver.implicitly_wait(10)  #隐式等待

driver.get('https://www.baidu.com')      # 请求网页
```

# 定位爬取元素
```
find=driver.find_element_by_class_name   #class
find=driver.find_element_by_id               #id
find=driver.find_element_by_tag_name  #html标签名
find=driver.find_element_by_name         #标签的name名
find=driver.fiind_element_by_css_selector  #css名为xxxxx （#header   xxxxx）如有两个元素以上被定义  如 .mxx  .sss   |  css名 为   .mxx.sss   空格去掉
find=driver.find_element_by_xpath  #使用xpath来定位，与xpath语法一样
find=driver.find_elements_by_link_text  #使用文字链即标签包含的文本文件精确匹配
find=driver.find_elements_by_partial_link_text  #使用文字链即标签包含的文本文件模糊匹配
find.send_key()
find.click()
```

