# Process

---

多进程操作：

```
第一种：第一个参数变化，其他参数不变化时适用
import multiprocessing
from functools import  partial

def test(can1,can2,can3):
	print(can1)
	print(can2)
	print('---')
	
pool = multiprocessing.Pool(processes=process_num) # process_num为进程数
pool.map(partial(函数名test，can2=参数2，can3=参数3), 首个参数can1的列表[can1,第二个进程can1])
pool.close()  # 关闭进程池，不再接受新的进程
pool.join()  # 主进程阻塞等待子进程的退出
---
第二种：所有参数都会变化时适用
from pathos.multiprocessing import ProcessingPool as Pool
def add_and_subtract(x,y):
      return x+y, x-y
      
res1 = Pool().map(add_and_subtract, range(0,20,2), range(-5,5,1))
[(-5, 5), (-2, 6), (1, 7), (4, 8), (7, 9), (10, 10), (13, 11), (16, 12), (19, 13), (22, 14)]
res2 = Pool().map(add_and_subtract, *zip(*res))
[(0, -10), (4, -8), (8, -6), (12, -4), (16, -2), (20, 0), (24, 2), (28, 4), (32, 6), (36, 8)]
```

多进程加锁（固定原本的输出顺序）

```
import multiprocessing
from functools import  partial

def test(can1,can2,lock):
	lock.acquire()
	print(can1)
	print(can2)
	print('---')
	lock.release()
	
pool = multiprocessing.Pool(processes=process_num) # process_num为进程数
lock=multiprocessing.Manager().Lock()
pool.map(partial(函数名test，can2=参数2,lock), 首个参数can1的列表[can1,第二个进程can1])
pool.close()  # 关闭进程池，不再接受新的进程
pool.join()  # 主进程阻塞等待子进程的退出
```

