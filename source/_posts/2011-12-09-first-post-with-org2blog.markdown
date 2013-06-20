---
comments: true
published: false
date: 2011-12-09 08:00:00
layout: post
slug: first-post-with-org2blog
title: 使用emacs org-mode写博客——org2blog配置指南
wordpress_id: 376
categories:
- Linux
tags:
- emacs
- howto
- org2blog
---

> 博客好久没有更新了，原因很多，最主要的应该是没有养成写文章的习惯，...还有一个很重要的原因就是从前写blog都是在线写的，虽然说不是很方便，但是在家的时候还可以忍受。可是到了教育网时，网速就完全无法忍受了，其次是在网页上撰写需要不停的使用鼠标，实在是很低效。因此博客长期没有更新。
现在情况有了不小的改观。在这几个月里我逐渐熟悉了emacs，同时必然会接触到emacs一大利器org-mode，使用org-mode可以非常方便的组织自己的工作，编写发布文章，十分强大。很自然的就想到如果使用org-mode来写博那该多好啊！
org2blog自然是首选！


废话不多说，简单介绍下org2blog的安装、配置和使用。





### org2blog的一些依赖








	
  * 需要[xml-rpc-el](http://launchpad.net/xml-rpc-el) 作为与wordpress通信

	
  * 需要高版本org-mode(我目前使用的org-mode是7.4版本，目前没有遇到什么问题)

	
  * 需要在你的wordpress中开启xml-rpc功能(`settings`–> `writing` –> `Remote Publishing` –> xml-rpc)








<!-- more -->





### 下载org2blog








	
  1. org2blog托管在github上，下载地址在[这里 ](https://github.com/punchagan/org2blog)，如果在你有git工具那么可以很方便的使用 `git clone http://github.com/punchagan/org2blog.git` 将el文件下载到当前的目录中。

	
  2. 下载后将org2blog文件夹放到.emacs.d或者其他你保存emacs插件的地方













### 修改emacs配置文件 `.emacs`






    
    ;org2blog
    (setq load-path (cons "~/.emacs.d/org2blog/" load-path))
    (require 'org2blog-autoloads)
    (setq org2blog/wp-blog-alist
          '(("wordpress"
             :url "http://username.wordpress.com/xmlrpc.php"
             :username "username"
             :default-title "Hello World"
             :default-categories ("org2blog" "emacs")
             :tags-as-categories nil)
            ("liuyix"
             :url "http://liuyix.com/wordpress/xmlrpc.php"
             :username "cnliuyix")))


上面是我的一个简单的修改，将第二个 `liuyix`, `url`, `username` 改成你自己的即可(可能是我没改好，也可能是有bug,我删除了第一个无效的wordpress配置后总是出现 `bad url` 的错误)












### 基本使用







#### 登录wordpress




[text] M-x org2blog/wp-login [/text]

按照提示输入密码即可登录。（进阶使用可以保存密码，直接登录）












#### 新建一个post/page




[text] M-x org2blog/wp-new-entry [/text]

这样org2blog会调用template添加了TITLE,CATEGORY,TAGS填写的地方，供填写












#### 保存为草稿/发布post/page








	
  * 以草稿形式上传到wordpress


[text] M-x org2blog/wp-post-buffer [/text]

	
  * 直接正式发布


[text] M-x org2blog/wp-post-buffer-and-publish [/text]












#### 现有文档的发布






org2blog还可以发布已经撰写好的org-mode编写的文档，实际上它和使用=org2blog/wp-new-entry=区别只在于没有模板生成的title,category,tags的信息，这些信息都是可选填写的，发布已有的org文档时，你可以手动加上诸如TITLE这样的属性。












#### 删除post/page








	
  * 如果在本buffer中已经有要删除的 `POSTID` ，那么删除post就是


[text] M-x org2blog/wp-delete-entry [/text]

同理已经删除page的操作是

[text] M-x org2blog/wp-delete-page [/text]

	
  * 如果要删除指定的POSTID的文章，则需要输入：


[text] C-u post-id M-x org2blog/wp-delete-entry [/text]












#### 修改post






和上面的删除类似类似，只要buffer中有POSTID信息，修改就是重新进行发布的操作，没什么特殊的。















### 一些实用tips







#### 在文中嵌入代码






这个要视你的wordpress使用的是什么插件了。一般常用的是使用*SyntaxHighlighter* ,因此在插入代码时需要选择使用下面的方法1

[text] @<pre lang=”lisp”>
(end-of-line)
@</pre> [/text]















### 总结






org2blog利用了wordpress的XMLRPC将org-mode变成了wordpress发文利器，只需要半小时时间就会熟练的掌握org-mode发博文。相信从此发博的效率会大增。












### 参考文献








	
  * [http://wdicc.com/about-org2blog/](http://wdicc.com/about-org2blog/)

	
  * [https://github.com/punchagan/org2blog](https://github.com/punchagan/org2blog)

	
  * [http://zhengdong.me/2011/01/13/hello-from-org2blog/](http://zhengdong.me/2011/01/13/hello-from-org2blog/)













## Footnotes:







1 [Hello, From org2blog@http://zhengdong.me](http://zhengdong.me/2011/01/13/hello-from-org2blog/)







