---
title: Python进程间通讯
date: 2018-12-27 15:15:47
tags:
 - Python
 - 编程技巧
---

# 闲聊
好久没有更新blog了，我可能都快忘记了（其实是懒），然后今天无聊的出奇，所以来学习点新东西吧。

哒哒 没错！就是Python的进程间通讯，好了 我们开始把。

# 正文
## 线程&进程
其实在Python中的多线程其实是假的，Python有一个GIL全局锁，以至于无法使用真正的多线程，所以呢很多情况下会去使用多进程，这里就涉及到了多个进程之间会涉及到共享数据，就引出了今天的话题，Python语言中的进程间通讯

## 第一种方式
### 0x01 多进程模块
Python使用多进程还是比较方便的，可以使用multiprocessing模块来实现。
首先通过模块引入需要的东西。我们先使用Queue的方式。
``` python
from multiprocessing import Process, Queue
```

<!-- more -->
### 0x02 完成写入数据的函数
``` Python
# 写数据进程执行的代码
def proc_write(q, urls):
    print('Process is write......')
    for url in urls:
        q.put(url)
        print('put %s to queue...' % url)
        time.sleep(random.random())
```

### 0x03 完成读取数据的函数
``` Python
# 读数据进程的代码
def proc_read(q):
    print('Process is reading......')
    while True:
        url = q.get(True)
        print('Get %s from queue' % url)
```

### 0x04 完成试验的主逻辑代码
``` python
if __name__ == "__main__":
    # 父进程创建Queue 并传给各个进程
    q = Queue()
    proc_write1 = Process(target=proc_write, args=(q,['url1', 'url2', 'url3']))
    proc_write2 = Process(target=proc_write, args=(q,['url4', 'url5']))
    prco_reader = Process(target=proc_read, args=(q,))

    # 启动子进程,写入
    proc_write1.start()
    proc_write2.start()

    prco_reader.start()
    
    # 等待proc_write1结束
    proc_write1.join()
    proc_write2.join()

    # proc_reader进程是死循环，强制结束
    prco_reader.terminate()
```

### 0x05 实验输出
``` bash
Process is write......
Process is write......
put url4 to queue...
put url1 to queue...
Process is reading......
Get url4 from queue
Get url1 from queue
put url2 to queue...
Get url2 from queue
put url3 to queue...
Get url3 from queue
Get url5 from queue
put url5 to queue...
```

## 第二种方式
### 0x01 多进程模块
第一种方式使用了Queue，第二种方式使用Pipe
``` python
import multiprocessing
```

### 0x02 写入的代码
``` python
#写数据进程执行的代码
def proc_send(pipe,urls):
    #print 'Process is write....'
    for url in urls:
        print('Process is send :%s' %url)
        pipe.send(url)
        time.sleep(random.random())
```

### 0x03 读取的代码
``` python
#读数据进程的代码
def proc_recv(pipe):
    while True:
        print('Process rev:%s' %pipe.recv())
        time.sleep(random.random())
```

### 0x04 主逻辑代码
``` python
if __name__ == '__main__':
    #父进程创建pipe，并传给各个子进程
    pipe = multiprocessing.Pipe()
    p1 = multiprocessing.Process(target=proc_send,args=(pipe[0],['url_'+str(i) for i in range(10) ]))
    p2 = multiprocessing.Process(target=proc_recv,args=(pipe[1],))
    #启动子进程，写入
    p1.start()
    p2.start()

    p1.join()
    p2.terminate()
```

### 0x05 实验输出
``` bash
Process is send :url_0
Process rev:url_0
Process is send :url_1
Process rev:url_1
Process is send :url_2
Process rev:url_2
Process is send :url_3
Process rev:url_3
```
