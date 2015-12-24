---
layout: post
title: Python并发实用编程手册[Draft]
date: 2015-12-17 07:08
comments: true
categories: Python
---

Python并发编程~~常用的~~builtin就是2个模块：`threading`和`multiprocessing`。其中`threading`因为著名的GIL，实际是*伪多线程*，每个thread并没有对应一个pthread；`multiprocessing`则是利用多进程的手段来绕过GIL达到并发的效果。

如果你的任务并非是CPU密集型，而是IO密集型或者网络应用的话——单线程时CPU总是处于等待的状态时，用threading其实影响不大。

<!--more-->

## threading

Doc: https://docs.python.org/2/library/threading.html

### Thread

和其他语言的线程创建类似，有两种方式创建线程的方式，一种是创建thread时传入要执行的工作方法，另外一种是创建`Thread`的子类。

#### join

`join()` 方法提供了不同线程间的协同功能。通常的用法是主线程在创建完所有的工作线程后，循坏调用没有工作线程的`join()`方法来等待所有线程的结束。`join()`方法还可以增加`timeout`参数设置超时时间，可以用来避免一个工作线程出问题使得整个程序死等的情况。

#### daemon

`daemon`是Thread的一个属性，程序退出不关心设置了`daemon`线程的『死活』。即只要所有非`daemon`线程都结束了，那么程序就可以结束掉了。
`daemon`线程类似于程序内部的『后台服务』，提供了程序运行时的『基础设施』，而不是程序工作流程链路中的部分。

## Lock, RLock

并发编程中，锁是基本原语。当有共享资源需要『互斥』访问时就要用锁来对这些资源进行保护。~~然而Python语言中由于GIL问题，实际上builtin的数据类型都是thread-safe的，使用时无需上锁~~对于mutable类型的变量在多线程共享使用时应该用Lock来控制并发，不能依赖Python的具体实现。

在Python 2.6以上，可以使用`with`简化获取和释放锁的过程，让代码更加简洁。

## Condition

是对Lock的一层封装。提供了`acquire()`, `release()`这两个Lock原语，还提供了`wait()`, `notify()`, `notifyAll()`这三个接口。

- `wait()` 是获得锁的线程主动释放锁，转入等待过程。
- `notify()` 是获得锁的一方不释放锁，但是会唤醒等待这把锁的其中一个线程。
- `notifyAll()` 类似`notify()`，不同的是不是唤醒一个，而是唤醒所有等待锁的线程。

典型的使用场景是生产者消费者模式。一个生产者，若干个消费者用一个队列来交互，这时候每个工作线程要想工作首先都需要尝试获得队列的锁。当一个消费者拿到了锁可以访问队列时发现队列时空的，这时候就要使用`wait()`来主动释放这把锁，然后将自己放到等待线程列表中等待；当一个生产者获得了队列的锁时，将数据放入到队列中，同时在释放锁之前调用`notify()`来通知其他等待这把锁的线程：『达令，有你快递儿~』，然后在释放锁。如果生产了多个数据，那么就可以使用`notifyAll()`通知所有的等待线程。

## Event

Event接口非常简单，就是`is_set()`和`set()`, Event用于在多线程间共享某一事件是否发生。我经常用来创建一个`stop_event`传给所有的worker线程，这样如果程序遇到异常或者其他需要终止的条件时，只要`stop_event.set()`，其他工作线程会循环的检查`stop_event.is_set()`。


## Semphore

上过操作系统课程的同学对『信号量』都有过接触，信号量和对应的`p`, `v`操作是并发程序的『操作原语』，即用这两个操作就可以表示所有的并发程序的设计和实现了。上述的Lock, Condition都可以看做是信号量的特定形式。

信号量由一个内部计数器和两个接口构成，内部的计数是非负数，对计数的操作：`release()`用于增加计数，`acquire()`用于减计数器。当计数器减到0时，`release()`操作就会阻塞直至其他工作线程完成`acquire()`。

Python的`acquire()`还支持可选参数`blocking`，当设置为True且计数器为0时，则会阻塞等待。


> 前面的叙述都算是对基本内容的解读，干货现在开始。

## 如何优雅的中断其他线程的任务


### 使用Event

在每个线程创建时传入`stop_event`,遇到异常或者到程序需要结束的时候，则`stop_event.set()`就可以了。
缺点：只有在线程完成一次工作后才会检查stop_event一次。因此如果线程工作比较久时会设置了`stop_event`也不会立刻结束。


```python

# worker

def do_some_job(job_q, stop_event):
	
	while not stop_event.is_set():
		try:
			do_foo()
		except:
			stop_event.set()


# manager

import Queue
thread_count = 4
stop_event = threading.Event()
job_queue = Queue.Queue()

threads = [threading.Thread(target=do_some_job, args=(job_queue, stop_event,)) for i in xrange(thread_count)]

for thr in threads:
	thr.start()

for thr in threads:
	thr.join()

```


## Signal的处理

TODO 多线程中Signal只能由**主线程**处理Signal。

- https://pymotw.com/2/signal/#signals-and-threads
- http://stackoverflow.com/questions/25676835/signal-handling-in-multi-threaded-python
- https://docs.python.org/2/library/signal.html

## multiprocessing - Process-based “threading” interface.

用多进程的方式来『模拟』threading的接口实现真正的并发程序。

TODO