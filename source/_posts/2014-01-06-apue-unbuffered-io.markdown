---
layout: post
title: "Linux Unbuffered IO"
date: 2014-01-06 01:09
comments: true
categories: Linux
published: false
---

## Linux无缓冲IO

> 本文是笔者阅读APUE以及Robert Love的<Linux System Programming Talking Directly to the Kernel and C Library>第二版的Unbuffered IO的总结笔记。

5个基本操作：
+ open
    + 参数
    + open的tricky用法：open始终返回的是可用的最小数值，因此可以关闭标准输入、标准输出、stderr再open则返回的数值是可以知道的。
        + 该种方法也是dup2的作用
+ read
    + read返回值大于0小于参数bufsize的原因
+ write
    + Unix, Linux的写机制：延迟写，write返回时只代表写入到了*缓存*中，是否已经写入到设备是未知的。
    + 
+ lseek
    + 空洞文件
+ close
