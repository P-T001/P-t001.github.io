# sqlserver 利用

---

**开启存储过程**

xp_cmdshell再sqlserver 2005之后默认禁用，如果有sa权限可以通过以下来开启

```
-- 启用xp_cmdshell（RECONFIGURE为重新配置）
# 允许配置高级选项
EXEC sp_configure 'show advanced options', 1;   
RECONFIGURE;   
# 启用xp_cmdshell
EXEC sp_configure 'xp_cmdshell', 1;  
RECONFIGURE;
EXEC sp_configure 'show advanced options', 0;   
RECONFIGURE;

-- 关闭xp_cmdshell
# 允许配置高级选项
EXEC sp_configure 'show advanced options', 1;   
RECONFIGURE;   
# 启用xp_cmdshell
EXEC sp_configure 'xp_cmdshell', 0;  
RECONFIGURE;
EXEC sp_configure 'show advanced options', 0;   
RECONFIGURE;
```

xp_cmdshell利用

```

```

