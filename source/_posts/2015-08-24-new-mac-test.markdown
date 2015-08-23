---
layout: post
title: "Octopress source迁移到新主机"
date: 2015-08-24 00:04
comments: true
categories: Other
---


- 新机器首先是把ssh key加入到github的setting
- git clone *liuyix.github.com*
- git checkout source
    - 操作完这一步后就相当于把当前octopress的source文档拉到了本地了。
- 安装octopress相关的ruby依赖等
	- 可选步骤：修改rubygems的安装源到国内的taobao源

完成上面几步后，就可以尝试调用`rake generate`生成一次网站，然后`rake deploy`看下是否成功~

-EOF-
