---
comments: true
published: false
date: 2012-02-25 18:40:00
layout: post
slug: python-gui-comparison
title: python GUI工具分析及选择–PyQT/PyGTK/wxPython比较
wordpress_id: 598
categories:
- Techs
tags:
- gui
- python
---

> python实在是非常好学好用的语言，适合个人做快速开发，做一些相对简单的、不要求性能，non-memory-critial的界面程序很适合。（大型程序如chromium这样的浏览器我觉得用python就有些不给力了。）
python GUI开发工具选择主要是pyqt,pygtk,wxPython这三个。本文就来比较一下这几个工具，从而根据个人需要选出一个合适的。


<!-- more -->





## PyQT







### Pros








	
  * 文档丰富

	
  * QTDesigner工具成熟

	
  * 跨平台是其突出点
















### Cons








	
  * Liscence问题:[开源协议介绍](http://www.awflasher.com/blog/archives/939)













### 使用PyQT开发的知名程序(摘自Wikipedia)








	
  * Anki, a spaced repetition flashcard program

	
  * **Eric** Python IDE

	
  * Kodos, Python Regular Expression Debugger

	
  * Orange, a data mining and visualization framework

	
  * qt-recordMyDesktop, Qt4 frontend for recordMyDesktop

	
  * Quantum GIS, a free software desktop Geographic Information Systems (GIS) application

	
  * Veusz, a scientific plotting application

	
  * Spyder, a lightweight Python IDE

	
  * Leo, an outliner and literate programming editor













## PyGTK







### Pros








	
  * 基于GNU LGPL













### Cons








	
  * 跨平台支持不佳：windows上移植不佳， **适合linux平台**

	
  * 据说界面不咋好看













### 使用PyGTK开发的知名程序








	
  * Anaconda installer

	
  * **BitTorrent**

	
  * Deluge

	
  * Emesene

	
  * Exaile

	
  * Flumotion

	
  * Gajim

	
  * gDesklets

	
  * **Gedit** (for optional Python subsystem and plugins)

	
  * **GIMP** (for optional Python scripts)

	
  * **GNOME Sudoku**

	
  * GRAMPS

	
  * **Gwibber (microblogging client)**

	
  * gPodder

	
  * Itaka

	
  * Jokosher

	
  * OpenERP

	
  * PiTiVi

	
  * PyMusique

	
  * PyChess

	
  * Pybliographer

	
  * ROX Desktop (includes ROX-Filer)

	
  * Smart Package Manager

	
  * Ubiquity (Ubuntu installer)

	
  * Wing IDE
















## wxPython







### Pros








	
  * 目前相比前两者来说，更流行(下文有验证)

	
  * 原生界面

	
  * 一个比较有价值的[链接](http://mach.debagua.com/archives/2009/0706_001023.html)













### 知名程序








	
  * BitTorrent, a peer-to-peer Bit Torrent application

	
  * Chandler, a Personal Information Manger

	
  * **Dropbox**, a storage provider/file synchroniser

	
  * Phatch, a Photo Batch Processor

	
  * Métamorphose - A batch renamer

	
  * TaskCoach, a Personal Information Manager

	
  * Editra, multi-platform text editor

	
  * Songpress, an application to generate guitar songbooks

	
  * **Ulipad**, programmer-oriented text editor

	
  * Whyteboard, free whiteboard and PDF annotator

	
  * Wrye Bash, a program for managing The Elder Scrolls IV: Oblivion "mods" and other related content

	
  * Digsby, All in one Instant messaging program.

	
  * pyMorinus, free astrology software using the Swiss Ephemeris

	
  * SOFA Statistics, a free statistics, analysis, & reporting program

	
  * Yet An Other Hex Editor, Arbitrary file size Hex Editor













### 学习资料








	
  * 啄木鸟社区翻译的[《wxPython In Action》](http://wiki.woodpecker.org.cn/moin/WxPythonInAction)
















## PyQT-PyGTK-wxPython三者的流行度比较————google trends + google search insight







### Fig-1:Google Search Insight






![http://liuyix.com/wordpress/wp-content/uploads/2012/02/wpid-gsi-04.png](http://liuyix.com/wordpress/wp-content/uploads/2012/02/wpid-gsi-04.png)

wxPython使用近几年一直在下滑，但是始终还是高于其他二者。PyQT在2008年前后有缓慢上升的趋势，也就是在那个时候超越了PyGTK。PyGTK可以说是一直在下滑。












### Fig-2:Google Search Insight






![http://liuyix.com/wordpress/wp-content/uploads/2012/02/wpid-gsi-1.png](http://liuyix.com/wordpress/wp-content/uploads/2012/02/wpid-gsi-1.png)

从上图就可以发现wxPython在韩国、中国亚洲地区很流行。












### Fig-3:Google Trends






![http://liuyix.com/wordpress/wp-content/uploads/2012/02/wpid-gt-0.png](http://liuyix.com/wordpress/wp-content/uploads/2012/02/wpid-gt-0.png)

这张图的结果和图1是大体相同的。注意此图中的地区排序是按pyqt进行的。















## 结论






从上面的分析，我们可以得出wxpython更加流行些，尤其是在国内。



	
  * 跨平台、丰富的文档,熟悉QT：PyQT

	
  * 跨平台、在意License：wxPython

	
  * 主要是在Linux平台，开源社区：PyGTK






