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

driver.get('https://www.baidu.com')           # 请求网页
driver.current_url                            # 获取当前url
driver.save_screenshot("tupian.png")          # 截图
driver.close()                                # 关闭当前页面，如果只有一个页面会关闭浏览器
```

# 定位爬取元素
```
find=driver.find_element_by_class_name('')           #定位class
find=driver.find_element_by_id('')                   #定位id
find=driver.find_element_by_tag_name('')             #html标签
find=driver.find_element_by_name('')                 #标签的name名
find=driver.fiind_element_by_css_selector('')        #使用css语法定位
find=driver.find_element_by_xpath('')                #使用xpath语法来定位
find=driver.find_elements_by_link_text('')           #使用文字链即标签包含的文本文件精确匹配
find=driver.find_elements_by_partial_link_text('')   #使用文字链即标签包含的文本文件模糊匹配

find.send_key()                               # 输入
find.click()                                  # 点击

```

鼠标动作链

```
#导入 ActionChains 类
from selenium.webdriver import ActionChains

# 鼠标移动到 ac 位置
ac = driver.find_element_by_xpath('element')
ActionChains(driver).move_to_element(ac).perform()


# 在 ac 位置单击
ac = driver.find_element_by_xpath("elementA")
ActionChains(driver).move_to_element(ac).click(ac).perform()

# 在 ac 位置双击
ac = driver.find_element_by_xpath("elementB")
ActionChains(driver).move_to_element(ac).double_click(ac).perform()

# 在 ac 位置右击
ac = driver.find_element_by_xpath("elementC")
ActionChains(driver).move_to_element(ac).context_click(ac).perform()

# 在 ac 位置左键单击hold住
ac = driver.find_element_by_xpath('elementF')
ActionChains(driver).move_to_element(ac).click_and_hold(ac).perform()

# 将 ac1 拖拽到 ac2 位置
ac1 = driver.find_element_by_xpath('elementD')
ac2 = driver.find_element_by_xpath('elementE')
ActionChains(driver).drag_and_drop(ac1, ac2).perform()
```

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        