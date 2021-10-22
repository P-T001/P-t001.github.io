# Pdfkit

---

- 介绍

  `pdfkit`可以将网页、html文件、字符串生成pdf文件。

- 安装

  ```
  pip install pdfkit
  pdfkit需要依赖wkhtmltopdf
  https://wkhtmltopdf.org/downloads.html
  安装后将bin路径加入环境变量
  ```
- 设置
  ```
  # wkhtmltopdf程序设置，如果加入环境变量可以不设置
path_wkthmltopdf = r'C:\\Program Files\\wkhtmltopdf\\bin\\wkhtmltopdf.exe'
  config = pdfkit.configuration(wkhtmltopdf=path_wkthmltopdf)
  # wkhtmltopdf参数设置，可以不加
  options = {
      'page-size': 'Letter',
      'margin-top': '0.75in',
      'margin-right': '0.75in',
      'margin-bottom': '0.75in',
      'margin-left': '0.75in',
      'encoding': "UTF-8",
      'custom-header' : [
          ('Accept-Encoding', 'gzip')
      ]
      'cookie': [
          ('cookie-name1', 'cookie-value1'),
          ('cookie-name2', 'cookie-value2'),
      ],
      'no-outline': None   # 等价于 --no-outline
      }
  
  pdfkit.from_file(html, to_file, configuration=config,options=options)
  
  一般设置：
  options = {
              'page-size': 'Letter', 'margin-top': '0.75in', 'margin-right': '0.75in',
              'margin-bottom': '0.75in', 'margin-left': '0.75in', 'encoding': "UTF-8",
              'custom-header': [('Accept-Encoding', 'gzip')],
              'cookie': [('cookie-name1', 'cookie-value1'), ('cookie-name2', 'cookie-value2'), ],
              'outline-depth': 10,
          }
  
  ```
- 使用
  ```
  import pdfkit
  import requests
  
  def html_to_pdf(path,url):
      '''
      功能：将url的html转成pdf
      :param path: 文件保存路径|str|如："./test.pdf"
      :param url: 需要转换的url|str|如："https://www.baidu.com/xxx/xxx.html"
      :return:
      '''
      response = requests.get(url)
      html = response.text
      html = html.replace('data-src', 'src')
      try:
          pdfkit.from_string(html, path)
      except:
          pass
          
  pdfkit.from_string(html代码,pdf输出路径)       # 字符串
  pdfkit.from_url(url,pdf输出路径)               # url
  pdfkit.from_file(本地html路径,pdf输出路径)      # 本地文件
  
  ```

- 问题

  ```
  使用from_url直接转会有问题，有时转出来的pdf会乱码
  ```

  