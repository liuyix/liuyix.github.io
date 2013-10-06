---
comments: true
published: true
date: 2011-05-02 21:10:50
layout: post
slug: vim-stl-auto-complete
title: 实现vim下的STL自动补全
wordpress_id: 251
categories:
- Linux
tags:
- vim
- 解决方法
---

vim的强大之处就在于可扩展性，换句话说就是“禁得起折腾”，不同于IDE的相对固定的快捷键等等设置。如果把IDE比作是豪华住宅，那么vim就是一个空荡荡的一座房屋，你必须要自己动手装潢，工具就是你对装潢的了解以及你的创造力，你的想象力。所以最后这个住宅能不能比上豪华住宅或者能否让你住的舒服完全要看你的动手能力了，呵呵，很激动人心的挑战啊（很适合喜欢DIY的coder  :-D ）

进入正题：vim中有一个非常有名的plugin——[omniCppComplete](http://www.vim.org/scripts/script.php?script_id=1520)（以下简称omni）,加上这个插件就可以实现自动补全struct,namespace的成员（实际也是应用强大的ctags），不过郁闷的是omni不支持STL的自动补全。这难不倒众多喜爱DIY的coder。<!-- more -->**仔细阅读omn的帮助文档，**你会发现实际上作者已经给出了如何让其自动不全STL（在FAQ中有提到），不过该方法还是很繁琐。幸运的是，已经有热心的coder为我们制作了相应的“插件补丁”——**[tags for std c++ (STL, streams, ...)](http://www.vim.org/scripts/script.php?script_id=2358)**，按照说明步骤一步一步操作就可以完成了。

具体方法：

	
  1. 将下载的压缩包cpp_src.tar.bz2解压，比如解压到 *~/src* `tar -jxf cpp_src.tar.bz2 -d ~/src`

	
  2. 打开终端，将work directory定位到~/src,然后运行以下命令`ctags -R --c++-kinds=+p --fields=+iaS --extra=+q --language-force=C++ cpp_src `

	
  3. 将生成的tags重命名：`mv tags a-new-name-tags`

	
  4. 在vim的环境中执行`:set tags+=/my/path/to/tags/cpp`


这样就可以在代码中自动补全STL代码了！Good Luck!

参考链接：[http://www.vim.org/scripts/script.php?script_id=2358](http://www.vim.org/scripts/script.php?script_id=2358)

尚未解决的问题：目前此插件只能实现对".""->"等的补全，但是不能补全"::" :-(
