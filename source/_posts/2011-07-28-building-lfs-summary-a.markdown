---
comments: true
published: false
date: 2011-07-28 10:02:44
layout: post
slug: building-lfs-summary-a
title: LFS的构建过程---LFS实践总结(一)
wordpress_id: 337
categories:
- Linux
tags:
- lfs
- toturial
---

![](http://www.linuxfromscratch.org/images/lfs-logo.png)

LFS是"Linux From Scratch"的简写，"from scratch"的本义是“从头开始”，这里应该是引申义,"从源代码构建"。LFS的主页上介绍为"Linux From Scratch (LFS) is a project that provides you with step-by-step instructions for building your own customized Linux system entirely from source."更多详细的介绍可以移步到[LFS Project Homepage](http://www.linuxfromscratch.org/lfs/)看看。

LFS主要的意义在于"教学"上，通过自己动手构建能更深入的认识linux，了解linux的运行原理。通过自己动手，还可以增强Linux上的操作水平。对于Linux的新手，LFS可能是一项比较“痛苦”的学习过程，因为你要使用大量的命令;对于使用过Linux一段时间的用户来说，构建LFS可以将Linux的零散的认识串起来，增强Linux的整体认识。

构建LFS的主要困难，我觉得对一看到E文就头大的童鞋来说，的确是nightmare。但我想喜爱折腾的，尤其是喜欢Linux的，E文都不会是大问题。除了语言的问题之外，得益于LFS文档的详尽和完美，我在构建的过程中没有遇到什么问题，很顺利。所以我觉得还是要认真读文档理解好就没什么问题。

<!-- more -->


## 简要的LFS构建过程


在分析构建过程之前，有必要说明下一些LFS-BOOK中重要的词汇。



	
  * toolchain:工具链，这是构建LFS中最重要的一个组成部分。它包含了编译程序的必要工具集，其中包括了assembler(汇编编译器)、compiler(编译器)、linker(链接器)等等。回忆一下在计算机的基础课程（操作系统、组成原理）讲述的构建程序的从源代码编辑到程序运行的完整过程，在这个过程中就用到了这些工具。只要保证了toolchain的正确无误，LFS的构建就成功了一大半了。

	
  * utilities:即我们在shell中各种linux工具。也包括构建程序所需要的一些必要的二进制工具。


为了在不同发行版上尝试构建LFS可以有结果一致性，即能参考同一个文档得到大致相同的结果(成功或者错误显示)，也为了达到少出错误的目的，采用了类似cross compile的方式的构建系统，简单讲就是多次的调整toolchain。


### LFS的构建步骤：





	
  1.  通过现有的toolchain环境，编译出“new and host-independent toolchain”。之所以这样是要保证后面的构建过程尽可能少的出错误，也可以保证在不同环境下进行的构建能有一个操作结果一致性的保障。

	
  2. 通过新的toolchain编译必要的工具(utilities)。第1步和第2步是第5章的主要内容。

	
  3. 通过以上2步实际上LFS的“地基”已经打好，下一步就要开始在上面“盖楼”了，这是第6章要做的工作。首先是进入mini Linux system(准备好环境后，通过chroot命令)，之后开始安装packages，（此过程相当于使用live-cd安装linux的过程，不同的是这里使用的是手动编译安装所有的package,而使用live-cd的安装过程是把已经编译好的packages复制到指定位置），**要理解linux的运行原理，实际就是理解Linux运行所需要的所有package的功能和内容。**

	
  4. 所有的package已经搭建好，现在还缺少引导程序，即启动脚本bootscript，这是第7章所讲的内容，通过启动脚本将package粘合在一起组成一个完整的系统。这其中比较重要的是udev的运行原理，其他的还有bootscripts,localtime,console,inputrc,bash,network。

	
  5.  最后的步骤就是编译内核并将新的内核添加到grub启动菜单中。


LFS的编译toolchain构建的顺序大体上是一样的：


> Linux-<version> API Headers--->Glibc--->Binutils--->GCC--->Utilities/Programs


这个顺序不能变。



	
  1. 将KERNEL对上层的“通信接口”--API接口 expose出来

	
  2. 通过API接口构建C库函数接口，Glibc提供了基本的管理内存、搜索目录、对文件的各种操作等功能

	
  3. Binutils提供了linker,assembler以及其他管理对象文件的工具

	
  4. GCC：C/C++编译器

	
  5. 至此就完成了toolchain的部署，其他软件都可以通过这个toolchain编译安装了。


这里列出的顺序相对位置是一定的，实际的构建过程还会设计一些细节，如GCC编译前需要编译MPFR，MPC等数学库函数

进一步概括LFS的构建过程就是先构建"干净的"toolchain，再通过toolchain编译必要的程序，然后编写启动脚本,编译kernel，最后将LFS添加到GRUB引导菜单中。是的，原理就是这么简单，难就难在面对一个实际系统构建中的各种细节。

我想将LFS弄明白的含义就是"我知道1)如何编译程序2)toolchain的构建过程3)Linux运行中重要的工具有哪些都有什么用4)重要的脚本配置。理解弄清这些内容，就可以进一步的玩转Linux！
