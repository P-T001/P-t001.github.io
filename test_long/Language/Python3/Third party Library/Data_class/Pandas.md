# Pandas

---

**保存数据**

​     保存数据一般使用csv，因为能保存很大，但是在windows上wps只能（csv/1,048,576行  ，xls/65,535行,xlsx/1,048,576行）

​     py3默认有csv /xls: pip install xlwt,xlrd /xlsx: pip install openpyxl

```
import pandas as pd  
# 第一种：
data1={'name':['aaa','bbb'],'age':['11','12']}
df = pd.DataFrame(data1)
header=list(data1.keys())
df.to_csv('test.csv', index=False, mode='a', header=header)

# 第二种
data2=[['name', 'age'], ['aaa', '11'], ['bbb', '12']]
df = pd.DataFrame(data2[1:])
header=data2[0]
df.to_csv('test.csv', index=False, mode='a', header=header)

# 第三种
data3=[{'name1': 'aaa','age':'11' },{'name1': 'bbb','age':'12'}]
df = pd.DataFrame(data3)
header=list(data3[0].keys())
df.to_csv(filename, index=False, mode=mo, header=header)  
# index=False 关闭索引;header=False 关闭表头，有则使用;mode模式w/a
# na_rep='null'  # 替换空值
```

**读取数据**



```

```

