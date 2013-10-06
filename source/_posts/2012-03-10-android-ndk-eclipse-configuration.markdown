---
comments: true
published: true
date: 2012-03-10 22:11:00
layout: post
slug: android-ndk-eclipse-configuration
title: Eclipse下配置NDK开发环境小结
wordpress_id: 643
categories:
- android
- dev
- Techs
tags:
- ndk
- tips
---

分享下最近几周我的一些NDK开发经验和心得。

Eclipse配置NDK环境，主要完成的功能使能调用Android NDK提供的工具链编译用C/C++源代码写好的共享库或者可执行的应用程序。由于我的工作需要的基本是完全native程序的编写，因此这里介绍的方法 **更适合编译Android下的本地应用程序或者共享库**

本文提供的方法皆非原创，在这里感谢原创作者的分享。





## NDK环境配置之前






Eclipse需要事先安装好 **CDT** ，本文在Ubuntu平台上测试可用。












## 最简单有效的方法————创建新的Builder






本方法是在Eclipse中调用NDK提供的 `ndk-build` 命令进行编译。综合这几周的开发，感觉还是这个方法是最靠谱的。因为你只需要编写一个Android.mk，无需考虑依赖关系，同时也最大程度的遵循了google提供的NDK build方法。









### 具体配置步骤








	
  * 新建一个C++ Project

	
  * 进入到这个project的 **Propertities** 选项中

	
  * **Builders** 一栏 –> **New** –> **Program**

	
  * 参考下面这张图进行配置，几个重要的地方：

	
    * **Location** 填入 `$NDK_HOME` /ndk-build 其中 `$NDK_BUILD` 是NDK安装的根目录

	
    * **Working Directory** 填入当前project的位置，可以通过选择 **Browse Workspace…** 选择

	
    * 可选步骤： **Arguments** 中写下需要传给ndk-build的参数

	
    * 如果要实现 _auto-build_ 可以在 **Refresh** 和 **Build Options** 中进行配置，我个人觉得auto-build对开发没有实际作用，因此这里就不介绍了。





简单几步就可以编译共享库了，够简单吧















## 参考链接






[Setting up Automatic NDK Builds in Eclipse](http://mobilepearls.com/labs/ndk-builder-in-eclipse/)












## 其他方法






这里还有一种我试验可用的方法，但是配置起来实在麻烦，适合移植已有程序或者开发大型项目时完全定制编译过程中使用。这里只给出出处，有兴趣的同学可以看看。



	
  * [http://www.srombauts.fr/2011/03/06/standalone-toolchain/](http://www.srombauts.fr/2011/03/06/standalone-toolchain/)






