---
comments: true
published: false
date: 2011-06-05 18:42:16
layout: post
slug: install-eclipse-swt-examples
title: Java SWT学习之Eclipse SWT Example(SWT示例)安装
categories: Java
tags:
- java
- swt
---

毕设需要写Java GUI,打算尝试一下SWT（虽然国内的资源异常的匮乏）。学习的最好方法就是看代码，看了一下SWT官网，哈哈，还真有许多SWT示例程序（不是snippets，而是完整的简单程序）
<!-- more -->
网址是：[http://www.eclipse.org/swt/examples.php](http://www.eclipse.org/swt/examples.php)

介绍里说有以下的示例程序：



	
  * ControlExample

	
  * CustomControlExample

	
  * AddressBook

	
  * BrowserExample

	
  * ClipboardExample

	
  * DNDExample (Drag and Drop)

	
  * FileViewer

	
  * GraphicsExample

	
  * HelloWorld [1-5]

	
  * HoverHelp

	
  * ImageAnalyzer

	
  * JavaViewer

	
  * LayoutExample

	
  * PaintExample

	
  * TextEditor

	
  * OLEExample (win32 only, OLE)

	
  * OleWebBrowser (win32 only, OLE)


这么多，这么丰富的源代码，非常的诱人~

由于是网站是英文的，所以此文主要是分享下自己根据这个英文指导一步步的安装过程，相当于一个汉化和简明教程吧 :-)

Examples安装可以有2个方式：

1.是在集成到eclipse作为SWT的demo，这样可以通过show view-->SWT Example,如下图所示，安装方法


[![](http://liuyix.com/wordpress/wp-content/uploads/2011/06/Show-View-_018-232x300.png)](http://liuyix.com/wordpress/wp-content/uploads/2011/06/Show-View-_018.png)


2.得到源代码，然后以Java Project导入到Eclipse中，通过Run as Application方式运行Example，如下图，安装方法

[![](http://liuyix.com/wordpress/wp-content/uploads/2011/06/SWT-Examples-Java-Project-156x300.png)](http://liuyix.com/wordpress/wp-content/uploads/2011/06/SWT-Examples-Java-Project.png)




## 一、以Eclipse插件形式安装

## 



	
  1. 进入Eclipse,Help → Install New Software...

	
  2. 通过"Eclipse Project Updates Sites"网站安装插件：我使用的Eclipse 3.5,所以相应的站点地址是[http://download.eclipse.org/eclipse/updates/3.5](http://download.eclipse.org/eclipse/updates/3.5)，记得要对应版本，如果你的是3.6,则网址的改成3.6

	
  3. 去掉下面的“Group items by category”

	
  4. 输入搜索“Eclipse SDK Examples”

	
  5. 找到后下载


如图

[![](http://liuyix.com/wordpress/wp-content/uploads/2011/06/Eclipse-SDK-Examples-Plug-in-Download-300x244.png)](http://liuyix.com/wordpress/wp-content/uploads/2011/06/Eclipse-SDK-Examples-Plug-in-Download.png)6.下载安装后重启下Eclipse。之后Window-->Show view-->Other-->SWT Examples即可！

参考网址：[Installing the examples](http://help.eclipse.org/galileo/index.jsp?topic=/org.eclipse.platform.doc.isv/samples/samples.html)




## 二、以源代码形式安装（推荐）





	
  1. 下载配置好独立的Swt库

	
    * [Eclipse SWT Download](http://www.eclipse.org/swt/) 从该页中的“Release”选择对应的平台下载

	
    * 以导入Existing Project方式导入到工作区：File-->Import-->Existing Projects into Workspace

	
    * 选择下载的zip文件，Project名称为默认的org.eclipse.swt




	
  2. 导入SWT Examples source

	
    1. 下载example: 在eclipse官网上下载“Example plugins” (如果你的版本是当前最新的release，在[这里](http://download.eclipse.org/eclipse/downloads/index.php),如果在该页找不到那就是在archived builds页里，在[这里](http://archive.eclipse.org/eclipse/downloads/index.php)

	
    2. 下载后解压缩，找到org.eclipse.swt.examples.source_[version].jar，再将该jar包解压缩

	
    3. 新建java project,导入源代码：File-->New-->Java Project-->名字任意取，关键是选择“Creating project from existing source”，选择你解压缩的jar包的路径里面的[jar包路径]/src，然后进行下一步

	
    4. 点击"Next"按钮，之后切换到Project标签，添加“org.eclipse.swt”（刚才导入的SWT的project），点击OK

	
    5. 点击Finish完成！




	
  3. 源代码导入完成，按道理是不会出现什么错误的。之后想要运行那个程序就右键点击相应的包（比如：org.eclipse.swt.examples.graphics）,选择run as-->Java Application（有可能存在多个main，选择一个即可）



