# ThreadPoolExecutor

---

多线程线程池demo：（写入文件时，可能部分内容被截断）

```

from concurrent import futures
from concurrent.futures import ThreadPoolExecutor

def task(n):
    print(n)
def task2(n,m):
	print(n,m)

def do_many_task_inorder():
    """多线程
    按任务发布顺序依次等待完成
    """
    url=[1,2,3,4,5]
    with ThreadPoolExecutor(max_workers=10) as executor:
    	future_list = [executor.submit(task, url) for url in urls]
    # 多参数写法
    args=[(1,2),(2,3),(4,5)]
    with ThreadPoolExecutor(max_workers=10) as executor:
    	future_list = [executor.submit(task2, num,url) for num,url in enumerate(urls)]

def do_many_task_disorder():
    """多线程执行
    先完成先显示
    """
    url=[1,2,3,4,5]
    with ThreadPoolExecutor(max_workers=10) as executor:
        future_list = [executor.submit(task, url) for url in urls]
        done_iter = futures.as_completed(future_list)  # generator
        

```

