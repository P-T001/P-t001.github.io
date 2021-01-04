# 爬虫类

---

爬虫主流：

```
Requests库  ：底层请求

Scrapy框架  ：框架联动

selenium库  ：模拟浏览器
```

HTML/XML解析器

```
BeautifulSoup :安装：pip install bs4      |导入：from bs4 import BeautifulSoup as BS
	html5lib  :安装：pip install html5lib
	lxml      :安装：pip install lxml	
配合使用：
req=requests.get('url')
response=BS(req.text,'lxml')
```







选择器：

**css**（http://www.scrapyd.cn/doc/185.html）

```
response.css(".xxxx a::attr(href)")  # .xxxx 代表class=xxxx 选取a标签href属性的内容
response.css("#xxxx a::attr(href)")  # #xxxx 代表id=xxxx 选取a标签href属性的内容
response.css('th::text')  #取th标签的内容
response.css('div#属性值') #取div标签的id属性为属性值
response.css('div[th]') #取div标签里有th属性的
response.css('div[id="123"]') #取div标签的id属性为123 |
response.css('div[id*="123"]') #取div标签的id属性包含123 |*可换成 ^开头；$结尾；

标签名::attr(属性名)
最后取值（列表或者字符串）
.extract()        #选取里面的值，列表形式  |.getall() ,获取不到则访问none
.extract_first()  #取第一个值，字符串      |.get()    ,获取不到则访问none


```

**xpath**（必须配合lxml使用）

```
// 从根节点选取  （节点:网页元素标签）
/ 从匹配选择的当前节点
. 选取当前节点
.. 选取当前的父节点
多级定位
    response.xpath('//table/tbody/tr/td')   //定位根目录开始所有的table的tbody的tr的td
跳级定位
    response.xpath('//table/tbody/tr[1]/td')  //定位根目录开始所有的table的tbody的tr第一行的td标签
依靠元素的属性定位
    response.xpath('//td[@class="mc_content"]')  //定位根目录开始所有的td的class属性是mc_content
    response.xpath('//td[@id="mc_content"]')  //定位根目录开始所有的td的id属性是mc_content
    response.xpath('//td[@id="mc_content"]/a[4]/text()')  //定位根目录开始所有td的id属性是mc_content，a标签第4位的文本
    response.xpath('//a[starts-with(@title,"注册时间")]') //定位根目录开始所有a的从属性title是“注册时间”
    response.xpath('//a[contains(text(),"闻")]') //定位到所有a的文本含‘闻’的字符串
提取元素或元素的属性值
    response.xpath('//a).extract() //提取a元素
    response.xpath('//a/text()').extract() //提取a元素的文本
    response.xpath('//a/@href').extract() //获取href的值

```

