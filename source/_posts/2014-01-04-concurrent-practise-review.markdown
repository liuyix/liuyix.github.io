---
layout: post
title: "并发编程理论与实践"
date: 2014-01-04 14:42
comments: true
categories: General
published: false
---

> 本文是*[SMP Primer for Android](http://developer.android.com/training/articles/smp.html)*的阅读笔记，该篇文章是由[@何_登成的一条微博](http://weibo.com/2216172320/AoTosDEUo)推荐的并发编程。

#### Changelog

|Version |  Time | Description |
| -- 
| 0.1 | 2014-01-04 | 笔记要点备忘，依旧施工中... 

<!--more-->

## 基本要点

+ x86的*Memory Consistency Model* 与 ARM的 _Memory Consistency Model_ 是不同的
+ ARM的 _Memory Consistency Model_ 更加relax，因此需要更多的控制。
+ 关于 _Observer_ 视角：什么是读一致，什么是写一致
+ 影响一致性的因素： _Cacheline_ ,_Compiler reorder_
+ _Memory barrier_
+ _RMW_ :_Read-Modify-Write_ / _CAS_ : _Compare And Set/Swap_
+ _Spinlock_ 和 _Release_ & _Acquire_
+ _Atomic_ & _Non-atomic_
+ C++的 _volatile_
+ _Java_ 的 _volatile_ 

## 并发问题

并发问题：真正的并发——SMP环境下同一时刻会有多条指令同时执行，共享变量——局部的和私有的变量不会出现并发问题，并发问题只有在 **共享变量** 上才会出现。因此无论在何种环境下一定要尽力减少 **共享** ，这是避免出现并发一致性问题的最好方法。
