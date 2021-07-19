# Information_search

---

目录：

{% include list.liquid all=true %}

---
**目录扫描**
- dirsearch
- 御剑
- 7kbscan
```
https://github.com/7kbstorm/7kbscan-WebPathBrute
```

**子域名挖掘**
- SubDomainsBrute
- Sublist3r
- https://phpinfo.me/domain/      
- https://github.com/shmilylty/OneForAll
- https://github.com/euphrat1ca/LayerDomainFinder

**漏洞扫描**

- Xray
- nessus
- awvs

提取网址js文件中的url和子域名

- https://github.com/Threezh1/JSFinder

  ```
  python JSFinder.py -f targets.txt -d -ou JSurl.txt -os JSdomain.txt  
  # -os 输出提取的子域名文件
  # -ou 输出提取的url文件
  # -d 表深度 1层
  ```

扫描ip和端口并进行对应服务弱口令爆破

- https://github.com/shadow1ng/fscan