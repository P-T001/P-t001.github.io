# Mssql Backup

---

Sqlserver（mssql）备份：



Sqlserver（mssql）还原：

<img src='https://p-t001.github.io/image/blog/Mssql-backup-1.png' align='left' style='width:500px;height:500px'>

<img src='https://p-t001.github.io/image/blog/Mssql-backup-2.png' align='left' style='width:900px;height:400px'>

<img src='https://p-t001.github.io/image/blog/Mssql-backup-3.png' align='left' style='width:1000px;height:250px'>

<img src='https://p-t001.github.io/image/blog/Mssql-backup-4.png' align='left' style='width:600px;height:300px'>



**CMD命令备份**

```
sqlcmd -S 127.0.0.1 -U sa -P 123  -E -Q "BACKUP DATABASE 数据库名 TO DISK='D:\xxx.bak'"
```

**CMD命令还原**

```
sqlcmd -S 127.0.0.1 -U sa -P 123  -E -Q "RESTORE DATABASE 数据库名 FROM DISK='D:\xxx.bak'"
```

