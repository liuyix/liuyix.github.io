---
layout: post
title: "Android Root 那些事"
date: 2013-07-14 19:14
comments: true
categories: android
---

## Root

所谓root就是在Android手机上获取最高权限，Android的底层就是Linux，因此Root过程就是普通Linux用户的提权过程。

## 获得Root的几个思路

+ 利用Android内核漏洞(实际上也是Linux的漏洞)进行提权
+ 使用`fastboot` 或者厂商提供的刷机工具(比如三星的 *Odin* )刷入修改的Kernel或者第三方的Recovery，再刷入root程序

## Root文件

+ su 
+ root权限管理应用: 如常用的Superuser.apk/SuperSU.apk

## Opensourced Superuser

Android Hack界大神Koush写了被广泛使用的Root管理软件: [Superuser](https://play.google.com/store/apps/details?id=com.noshufou.android.su&hl=en)
Koush的Superuser由于Cyanogenmod的一部分，因此是开源的。地址：[https://github.com/koush/Superuser](https://github.com/koush/Superuser)  
阅读代码我们就可以了解Android的Root管理应用以及su原理以及如何实现的。

未完待续...
