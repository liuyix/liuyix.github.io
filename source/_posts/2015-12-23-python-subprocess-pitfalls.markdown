---
layout: post
title: Python中的subprocess与Pipe
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

## 探究实现

Python在系统编程领域可以理解为就是C语言的一种简写，因为无论是用C语言还是Python都是对系统Linux/Windows API的使用，只是相比于C，Python封装后由于是解释型语言而变得易于编写和调试。

在Python中subprocess是用来创建新的进程，同时创建管道连接子进程的stdout, stderr, stdin（可选）。然后执行子进程，最后得到子进程的return code。

> This module intends to replace several older modules and functions:
> os.system
> os.spawn*
> os.popen*
> popen2.*
> commands.*

所以可以理解为Python意图用subprocess模块来统一之前若干生成子进程的方式。

关于subprocess的基础用法再次暂时略过，网上相关的内容很多，有时间再赘述。这里重点说一下shell多管道流对应的python实现。

### 一个shell多管道脚本的改写

shell编程领域，将cli工具结合强大的pipe，可以一行代码就能完成相对复杂的工作，尤其是在文本编辑上。如以下的例子：

```
ps aux | egrep 'xtrabackup|innobackupex' | grep -v grep | awk '{print $2}' | xargs kill
```

这是（我比较常用的）杀掉备份进程的一行命令。大致流程如下图所示。

![流程图](/images/0105-1.svg)

那么如果如何将上述代码转换为python脚本表达呢？

推荐的做法：分别生成subprocess子进程，同时用管道相连。

```
import subprocess
import shlex
ps_proc = subprocess.Popen(shlex.split('ps aux'), stdout=subprocess.PIPE)
grep_proc = subprocess.Popen(shlex.split("egrep 'xtrabackup|innobackupex'"), stdin=ps_proc.stdout, stdout=subprocess.PIPE)
awk_proc = subprocess.Popen(shlex.split('awk "{print $2}"'), stdin=grep_proc.stdout, stdout=subprocess.PIPE)
kill_proc = subprocess.Popen(shlex.split('xargs kill'), stdin=awk_proc.stdout)
```

每一个子进程的`stdin`都是上一个子进程的`stdout`，除最后一个子进程外其余进程的stdout参数都是`subprocess.PIPE`即管道输出，这样就首先了首尾相连。