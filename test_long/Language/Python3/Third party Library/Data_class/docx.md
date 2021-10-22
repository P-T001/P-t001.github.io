# docx

---

- 介绍：用作按照模板生成大量同类型文档

- 来源：https://mp.weixin.qq.com/s/UqTam2nqxs8fke1EoXx-CQ

- 安装与导入：

  ```
  pip install docx-mailmerge
  from mailmerge import MailMerge
  ```

- 操作

  ```
  创建一个word，内容“此_同事,在_年薪资为_元。”
  在第一处_插入域/域名为MergeField/域名为Name
  在第二处_插入域/域名为MergeField/域名为year
  在第三处_插入域/域名为MergeField/域名为money
  变成：“此<<name>>同事,在<<year>>年薪资为<<money>>元。”
  代码：（单个生成，也可以设置个列表进行批量生成）
  from mailmerge import MailMerge
  template = '薪资证明模板.docx'
  document = MailMerge(template)
  document.merge(name = '唐星',
                 year = '2020',
                 money = '11111'
  )
  document.write('生成的1份证明.docx')
  ```

  题外：word转pdf
  
  - 安装与导入：
  
    ```
    pip install pypiwin32
    -----
    import win32com
    from win32com.client import Dispatch, constants
    ```
  
  - 操作
  
  ```
  import win32com
  from win32com.client import Dispatch, constants
  import os
  
  # 生成Pdf文件
  def Docx_to_PDF(docx_path,pdf_path):
      word = Dispatch("Word.Application")
      word.Visible = 0  # 后台运行，不显示
      word.DisplayAlerts = 0  # 不警告
      doc = word.Documents.Open(docx_path) # 打开一个已有的word文档
      doc.SaveAs(pdf_path, 17)  # txt=4, html=10, docx=16， pdf=17
      doc.Close()
      word.Quit()
  ```
  
  

