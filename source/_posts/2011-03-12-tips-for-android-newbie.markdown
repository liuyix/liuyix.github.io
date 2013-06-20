---
comments: true
published: false
date: 2011-03-12 17:51:23
layout: post
slug: tips-for-android-newbie
title: Android初学者最易遇到的麻烦——Android开发环境相关问题集锦
wordpress_id: 102
categories:
- Techs
tags:
- android
---

> 

> 
> 初识Android有一段时间了，遇到了好多纠结的问题，这些问题应该说具有一定的普遍性的（可以通过[google](http://www.google.com.hk)比较容易的找到答案）。在这里我一一列举下我目前已经遇到的问题。
> 
> 





## 关于AVD（Android Virtual Device android模拟器）




**问题描述：**初次安装很可能会出现：**ERROR: unknown virtual device name: 'XXXXXX'。**这种问题通常发生在Windows系列平台上。




**问题原因**：“我的文档”的默认保存位置改变，而AVD依然在系统默认的位置（即C:\Users\你的用户名\）上查找，因此找不到已经创建的模拟器。




**解决方案**：更改环境变量，在系统环境变量中增加变量名为"**ANDROID_SDK_HOME**"(生成的模拟器文件放置的位置)的系统变量，从而使生成路径与查找路径一致。





## 关于Eclipse版本的选择——现阶段不要选择Eclipse 3.6,最好选择3.5,3.4




**问题描述**：Eclipse+ADT环境下，**自动代码补全功能异常缓慢，Eclipse因而常常出现假死的情况**




这个问题是困扰了我很久的最纠结的问题了，起初以为是传说中的“Eclipse吃内存，资源消耗大”，同时也不怎么影响使用，所以就没有当回事。可是用久了就有些不耐烦了，老是自己等Eclipse，这种滋味很难受！由于这样的问题不好用关键词描述，所以寻找答案的过程比较漫长，大概用了几个小时吧。最后终于在eoeAndroid上找到了答案（感谢eoeAndroid社区！）




**问题原因**：Eclipse 3.6与ADT存在已知bug，目前暂未修复。——从中也体会到了一点，软件不是越新越好……




**解决方案**：有2种解决办法，第一种是治标的——将代码自动补全功能时间调长些；第二种比较痛快——直接卸载掉Eclipse 3.6,换成Eclipse 3.5即可。





### 小弟毕竟是初学几个月，因此目前遇到的就是这2个问题，欢迎大家补充！！






