```
定时任务:schtasks /create /RL HIGHEST /F /tn "Windows Server Update" /tr "c:\windows\Temp\xxx.exe" /sc DAILY /mo 1 /ST 09:00 /RU SYSTEM
```