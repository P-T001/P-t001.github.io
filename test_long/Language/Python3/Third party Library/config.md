# config

---

- 配置文件读取1：

  只会把配置文件参数读取成字符串

```
from configparser import ConfigParser
import os

def read_config(file_path):
    conn = ConfigParser()
    if not os.path.exists(file_path):
        raise FileNotFoundError("%s配置文件不存在"%file_path)
    conn.read(file_path)
    return conn

if __name__ == '__main__':
    config_result=read_config('test.ini')
    print(config_result.get('api','xxx'))
```

​	test.ini

```
;这是配置文件注释符
[api]
xxx=123
```

- 配置文件读取2：

  读取配置文件参数并保留其数据类型

```
import config
config.XXXXXX
```

​	config.py(在项目环境的根目录)

```
NUM=123
ZFC="字符串"
```

