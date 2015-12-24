---
layout: post
title: 总结subprocess与pipe
date: 2015-12-23 21:31
comments: true
categories: Python
---

## 一、纠结的困境

Python在多进程上不是很令人满意，尤其是`subprocess`模块。当用Python实现一个shell脚本中的管道时就出现了比较尴尬的局面。

### 大数据量的管道问题

subprocess模块有两种方式来和生成的子进程交互：`wait`和`communicate`。
关于`wait`文档中有以下说明：
> Warning This will deadlock when using stdout=PIPE and/or stderr=PIPE and the child process generates enough output to a pipe such that it blocks waiting for the OS pipe buffer to accept more data. Use communicate() to avoid that.

即当stdout/stdin设置为PIPE时，使用`wait()`可能会导致死锁。因而建议使用`communicate`

而对于`communicate`，文档又给出：
> Note The data read is buffered in memory, so do not use this method if the data size is large or unlimited.

`communicate`会把数据读入内存缓存下来，所以当数据很大或者是无限的数据时不要使用。

那么问题来了：当你要使用Python的`subprocess.Popen`实现命令行之间的管道传输，同时数据源又非常大（比如读取上GB的文本或者无尽的网络流）时，官方文档不建议用`wait`，同时`communicate`还可能把内存撑爆... ![/images/1.jpg](/images/1.jpg)

