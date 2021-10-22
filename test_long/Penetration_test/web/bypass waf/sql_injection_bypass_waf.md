# Sql_injection_bypass_waf

---

bypass 云锁（2020.12）

请求方式get->post即可，不会检查url（但url还是原本可以注入的语句），只会检测postdata（需要该请求支持post）

bypass 宝塔（2021.1）

请求方式post，脏数据，数据包过大宝塔会跳过检测