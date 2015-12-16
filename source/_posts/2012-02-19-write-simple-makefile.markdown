---
comments: true
published: true
date: 2012-02-19 20:02:00
layout: post
slug: write-simple-makefile
title: makefile简单入门
wordpress_id: 551
categories:
- Linux
tags:
- makefile
---

> 在linux上混了这么久，真成混的了，连makefile都没有学习过，惭愧啊～作为makefile的快速入门指南，本文是我个人学习makefile时做的笔，此为第一篇。后续会有更加详细深入的学习总结。







## 导言






make程序可以算得上是一个domain specific language，完全是一个完整的脚本语言，make是linux,unix上编译 **等** 工作的标准工具，对于复杂的程序来说，可以智能的、自动化完成复杂的程序编译工作。而需要就是编写一个directive的脚本——makefile告诉编译器和其他工具应该如何编译project。 本篇是陈皓写的“跟我一起写makefile”的第一部分的总结，比较凌乱…

## 学习资料
	
  * 陈皓——“跟我一起写makefile”	
  * how to write a simple makefile<!-- more -->

## makefile的最基本编写规则
    
    target : prerequisites
        command


这个就是makefile最基本的编写规则，后续的讲解以及makefile的更多写法不过是为了进一步简化这个规则的编写。也就是说你只要把这个规则弄懂了，makefile你就会写了，和makefile高手，你差得就是一些技巧和高级用法了。但起码你会写makefile了。

	
  * **target** 就是要构建的目标——可以是C/C++的object，可以是目标程序，也可以是一个标签。

	
  * **prerequistites** 是构建 **target** 需要的文件。对object来说，它也许是c，c++源文件； **target** 是目标程序，那么它就是object文件（.o文件）

	
  * **command** 是将 **prerequistites** 变成 **target** 的方法


一言以弊之，target是output,prerequisites是输入，command是过程方法。 值得注意的是command必须以一个TAB键作为开始，否则会出现"遗漏分隔符。停止"的错误。

### hello-makefile的makefile

首先编写一个hello-makefile.c，内容我想就不用我写了吧…之后在存放hello-makefile的目录下创建一个 _Makefile_文件(注意没有扩展名)。 Makefile内容如下：

```makefile    
    hello-makefile:hello-makefile.o
        cc -o hello-makefile hello-makefile.o
    hello-makefile.o: hello-makefile.c
        cc -o hello-makefile.o hello-makefile.c
    clean:
        rm *.o hello-makefile
```

## TAB键、反斜杠(/)

	
  * TAB键在makefile中是command开头的分割符，这在前文已有讲述。

  * 反斜杠（/）用来断行，即一行没有写下或者为了美观而将 `command` 或者 `prerequistites` 拆成几行来写。刚学习写makefile时可能会忘掉而出现错误。

## make不仅仅可以做编译

target可以是目标文件、二进制程序，也可以是一个label，后面没有prerequisites，可以让makefile如同shellscript一样完成其他工作（备份、打包）。比如说我们经常使用的 `make clean` 实际上是利用make完成shell脚本一样的工作。

## 使用变量，简化书写，减少bug
    
    objects = main.o kbd.o command.o display.o \
    insert.o search.o files.o utils.o


以后使用时就使用 **$(objects)**


## 自动推导


**.PHONY** 表示clean是一个伪目标文件

## 编写makefile好习惯


每个makefile中都 _应该_ 定义一个clean命令，用于清空从前的编译产生的文件。


