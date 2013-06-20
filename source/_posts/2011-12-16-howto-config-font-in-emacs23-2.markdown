---
comments: true
published: false
date: 2011-12-16 13:22:00
layout: post
slug: howto-config-font-in-emacs23-2
title: Emacs23 字体配置
wordpress_id: 426
categories:
- Linux
tags:
- configure
- emacs
---

> 前几天使用org2blog出了一些莫名的问题，经过一系列的折腾（编译安装emacs,源码安装org-mode），还是没有搞清楚问题出在哪儿了，但是现在org2blog又不明原因的恢复正常了！（对emacs不了解的人伤不起啊，有时间一定要仔细研究下）


emacs23中默认的字体很小,此文告诉你如何用最"业余"也是很简便的方式添加修改emacs配置～
<!-- more -->



	
  1. 打开emacs，菜单栏中选择 **Options** –> **Set Default Font…**

	
  2. 在弹出的对话框中挑选好字体以及大小

	
  3. 在任意文本下,将光标停在修改后的文字上面

	
  4. 输入命令:

    
    M-x describe-font




	
  5. 复制 **name(open by):** 后面的内容，比如说是



    
    -unknown-DejaVu Sans Mono-normal-normal-normal-*-16-*-*-*-m-0-iso10646-1





	
  1. 根据(5)，将



    
    (set default-font "-unknown-DejaVu Sans Mono-normal-normal-normal-*-16-*-*-*-m-0-iso10646-1")


这一句添加到 *.emacs*配置文件中



	
  1. 重启emacs就会看到效果！


Gook luck!


## Update 2013-3-16

### 字体设置没有可移植性

在多个机子上迁移emacs时需要将字体设置部分注释掉，不然会出现 *emacs正常启动，但是配色显示不正常*的现象。

### 更傻瓜的设置方式

全部用界面菜单操作更方便。  

1. `Options` --> `Set Default Font`
2. 选择满意的字体之后，保存设置 `Options` --> `Save options`


### 参考文章

[设置Emacs的字体](http://blog.waterlin.org/articles/%E8%AE%BE%E7%BD%AEemacs%E7%9A%84%E5%AD%97%E4%BD%93.html)

