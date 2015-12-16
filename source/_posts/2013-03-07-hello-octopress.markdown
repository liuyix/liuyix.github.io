---
layout: post
title: "Hello Octopress!"
date: 2013-03-07 18:45
comments: true
published: true
external-url: 
categories: Octopress
---

{% img /images/octopress-logo.png  %}

##   初识Octopress

忙里偷闲，折腾下Octopress～
{% blockquote  http://octopress.org  %}
Octopress is a framework designed by Brandon Mathis for Jekyll, the blog aware static site generator powering Github Pages.
{% endblockquote  %}
Octopress说白了就是一个可以使用markdown[^markdown]写博客的静态网页生成后端。而且还可以利用[github pages](http://pages.github.com/ 'github pages')做自己的博客。  
使用了一段时间的Wordpress写博客，然后写着写着就没有然后了。没有坚持下来的原因很大一部分是因为自己，当然(很喜欢这个“当然”)Wordpress不爽体验也是一个原因。这促使我考虑Wordpress的替代方案。

### [吐槽]从Wordpress转移到Octopress的原因

吐槽Wordpress各种不爽之前，先声明这不是技术上的比较，也不是产品上的优劣比较，我只是从个人需求的角度说一下Wordpress不适合写技术博客，也可以说不能快速的书写有质量的文章。 
简单的说Wordpress写博客，需要离开编辑器，操作不便，还要操心其他不相关的事。  

<!--more-->

####   不能很方便的(在emacs里)写博客

{% pullquote  %}
程序员优点之一就是 *“懒”* ，自然写博客也懒得离开编辑器在网页上码字，而且网页上码字体验远不如顺手的编辑器，还必须要联网，最让人受不了的就是手要离开键盘，用 *鼠标* 来进行各种操作！（Windows用户你不会理解的...）。  
{"Wordpress写博客，需要离开编辑器，操作不便，还要操心其他不相关的事。"}
使用Wordpress的这段时间里，我一直在不停的探索如何更高效更舒服的：从最初的网页上的编辑器插件，到搜索各种Linux,Windows客户端( [菊子曰][juziyue]是这一时期的终点，使用上很适合非程序员，但不幸的是只有Windows版本), 最终遇到了org2blog——使用emacs org-mode来写博客。经过我持续不懈的折腾，Wordpress这个诟病基本被我解决掉了。  
{% endpullquote %}

#####   Octopress Side

Octopress前端支持markdown类的语法，和org-mode相比，同样适合编写格式化的文档，语法相似，更加精简。更欢乐的是markdown文本非常具有可读性（这也是markdown的设计哲学）。  
不仅如此，依托于github，博客文章还具有云端 *增量备份* 的功能。这点和Wordpress不同，Wordpress上写好的内容用以HTML方式存入MySQL数据库，虽然也有备份的功能，可本地化特点的缺失，*需要离开编辑器操作* 实在是个鸡肋。
写作之后的同步操作也无需离开编辑器，几条命令就搞定网站！

####   需要购买主机

这是使用Wordpress写博客首先需要操心的事。搭建需要花钱买主机停放你的站点，虽然成本不高，但也不是无成本的。我目前的消费水平还不足以为了一个每天只有不到100IP的小站点购买VPS，需要精打细算——不仅要选择哪家主机划算，还要花折腾主机，还时不时地担心自己或者服务商或者同IP的莫个站点被GFW墙掉。总之一个字“累”！

##### Octopress Side

首先是免费，其次还不如管访问延时等主机相关的问题了。还记得曾有一段时间为了优化访问，花了很多精力在减少插件、优化插件、压缩网页上。虽然建站的很多东西，again, 和写博客是无关的。相比之下，Octopress实际最后就是静态的网页而非动态网站，所以不需要进行优化。

####   博客的配置相对复杂

玩过Wordpress的人都明白平时最常折腾的就是插件和主题，还有Wordpress的升级。  
对于只想简简单单写技术博客，写日记，发牢骚的人来说，这些也是额外需要费心思的地方，而且没点时间和技术，博客还会显得丑陋不堪，缺乏美感。 

##### Octopress Side

认识Octopress就是在一次搜索时看到一个技术博客，那个博客让我眼前一亮——简洁、大方，没有大多数Wordpress博客给人的花哨之感，很对程序员的胃口，仔细读了那个博客，才知道除了Wordpress还有一个叫Octopress的东东。  
Octopress在界面上完成度很高，可以说不需要任何修改，其简约之美也足以媲美大多数的Wordpress主题。于是可以更加专注于内容。  


第一次写Octopress，各种不熟练，花了好久。就先写到这里，有时间再写下自己的配置过程。


[juziyue]: http://sns.juziyue.com '菊子曰的网站'

**********

[^markdown]:  [http://en.wikipedia.org/wiki/Markdown]
