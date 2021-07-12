# argparse

---

用法：命令行运行时，获取对应参数来运行功能

```
import argparse
if __name__=="__main__":
	parset=argparse.ArgumentParser(description="介绍")
	parser.add_argument('-u', '--url', help='帮助信息')
    parser.add_argument('-v', '--version', type=int,
                        choices=[3, 5], default=3, help="thinkphp version, default 3")
    parser.add_argument('-p', '--path', type=str, help='log path')
    parser.add_argument('-y', '--year', type=int, default=datetime.datetime.now().year, help="datetime start year, default this year")
    parser.add_argument('-m', '--month', type=int, default=datetime.datetime.now().month, help="datetime start month, default this month")
    parser.add_argument('-d', '--day', type=int, default=1, help="datetime start day, default 1")

    args = parser.parse_args()
    args.url         # 获取url参数
    args.version     # 获取version参数
```



