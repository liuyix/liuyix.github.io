---
layout: post
title: "Octopress迁移到新主机"
date: 2015-08-24 00:04
comments: true
categories: Octopress
---

- 新机器上首先是把ssh key加入到github的setting，然后配置好基本的git信息（email, name），此处步骤略过。可以参考：[https://help.github.com/articles/set-up-git/](https://help.github.com/articles/set-up-git/)
- `git clone -b source git@github.com:username/username.github.com.git octopress`
    - 操作完这一步后就相当于把当前octopress的source文档拉到了本地了。
    - **这一步操作前一定要确保在其他机器上的markdown文件以及其他配置文件的修改都已经push到source分支了，否则这一步会导致博客文章丢失！！！**
- 进入到octopress, 然后`git clone git@github.com:username/username.github.com.git _deploy`
	- 这一步是在`_deploy`建立好指向master分支的git仓库，方便之后发布文章时使用
- 安装octopress相关的ruby依赖等
	- 建议修改rubygems的安装源到国内的taobao源，详细操作步骤：[http://ruby.taobao.org/](http://ruby.taobao.org/)，默认的rubygems.org源已经被墙，速度很慢。

完成上面几步后，就可以尝试调用`rake generate`生成一次网站，然后`rake deploy`看下是否成功~

### 在不同主机上使用Octopress上发布文章

每次发布新的文章或者修改现有文章时，需要把`source`分支的修改（即octopress目录所指向的git仓库分支）commit并且push到github上，之后在另外的主机上首先进入到octopress目录，在编辑文章前首先`git pull`下拉取修改。这样的编辑才能连贯，不然会发生文章丢失的情况。

Reference:

- [Clone Your Octopress to Blog From Two Places](http://blog.zerosharp.com/clone-your-octopress-to-blog-from-two-places/)

-EOF-
