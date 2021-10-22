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
chrome：https://chromedriver.storage.googleapis.com/index.html
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
from selenium.webdriver.chrome.options import Options
import time

chrome_options = Options()
chrome_options.add_argument('--headless')  # 隐藏后台运行
driver = webdriver.Chrome(executable_path=selenium_path,chrome_options=chrome_options)
driver.get(m_li[1])
# 调用js进行循环下滑每次step=50，下滑到底为止
strs=""" 
        (function () { 
            var y = document.body.scrollTop; 
            var step = 50;   
            window.scroll(0, y); 
            function f() { 
                if (y < document.body.scrollHeight) { 
                    y += step; 
                    window.scroll(0, y); 
                    setTimeout(f, 50); 
                }
                else { 
                    window.scroll(0, y); 
                    document.title += "scroll-done"; 
                } 
            } 
            setTimeout(f, 1000); 
        })(); 
        """
driver.execute_script(strs)
time.sleep(5)
# 保存成mhtml
res = driver.execute_cdp_cmd('Page.captureSnapshot', {})
with open(m_li[0], 'w') as f:
    f.write(res['data'].replace('\r',''))
driver.quit()
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
urls = driver.find_elements_by_xpath("//a")   # 抓取所有超链接
for url in urls:
    print(url.get_attribute("href"))
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


# 鼠标滑动 
window.scrollBy(0,500)  # 向下滑动500个像素
window.scrollBy(0,-500)　# 向上滚动500个像素
window.scrollBy(500,0)  # 向右滑动500个像素
window.scrollBy(-500,0)　# 向左滚动500个像素
driver.execute_script("window.scrollTo(x,y)")  # 滑动到具体位置。调用js来滑动
driver.execute_script("arguments[0].scrollIntoView();", element)  # 向下滚动至-元素可见
driver.execute_script("arguments[0].scrollIntoView(false);", element)  # 向上滚动至-元素可见
js="window.scrollTo(0,-document.body.scrollHeight)" 
driver.execute_script(js)  # 滑动至页面底部
js="window.scrollTo(0,document.body.scrollHeight)" 
driver.execute_script(js)  # 滑动至顶部
```

​                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        