---
comments: true
published: false
date: 2011-04-21 09:32:33
layout: post
slug: modify-hosts-to-use-google
title: '[2012-2-5-更新]修改hosts访问google的各种服务(groups,docs...)'
wordpress_id: 188
categories:
- General
tags:
- gfw
- google
- hosts
- windows
---

==================================================================================================================


### 2012-2-5 更新


此次更新也许是最终更新了（别担心，亲，这是好消息，偶已经找到一劳永逸的方法喽~）


### 最省事的方法——使用免费VPN


[![](http://liuyix.com/wordpress/wp-content/uploads/2011/04/podvpn-logo-300x50.png)](http://liuyix.com/wordpress/wp-content/uploads/2011/04/podvpn-logo.png)

穿越，我一直在使用的**[豆荚VPN](http://www.podvpn4.info/)**，一直灰常稳定，给力！强烈推荐。该VPN免费账户，每月有800M的流量，对于平时浏览网站什么的足够用了。


#### **豆荚VPN的几个突出优势**





	
  * 有良好的服务支持：豆荚VPN有QQ群支持以及新浪微博，VIP用户也有专属QQ群。而且服务快速、热情。

	
  * 给力的windows客户端：具有**自动更新**功能的windows客户端（有了自动更新功能，就不必再担心河蟹了）




#### 使用VPN的一些缺憾





	
  * 速度上不如修改hosts快




### 速度最快的方式——修改hosts


传统的穿越方法。使用VPN的一个缺憾就是速度的问题，使用此方法可以弥补该不足。

推荐给只需要访问google及google的所有服务,facebook,twitter,wiki等国外主流网站的用户。

之前文章里只给出了具体的hosts文件，可是hosts是需要与时俱进的。这点难不倒技术男！


#### 请出主角——[smarthosts](http://code.google.com/p/smarthosts/)


这是google code上的一个开源项目，地址:[http://code.google.com/p/smarthosts/](http://code.google.com/p/smarthosts/)。


> SmartHosts是一个在Google Code上维护更新的Hosts文件。作者为了炒概念，不要脸地把它叫做了“云hosts”。

本项目还提供简单方便的一键更新程序，方便您更新您的hosts。[程序更新中]


如果google code打不开，smarthosts上提供了一个镜像：[https://smarthosts.sinaapp.com/](https://smarthosts.sinaapp.com/) （这个镜像相信很难被和*谐了）


#### 使用Hosts文件的缺憾





	
  * 可访问的站点有限




### 教育网的“尊贵特权”——使用ipv6实现穿越


曾有人戏称，我天-河蟹-朝教育网是全球最大的ipv6商业网。这点确实不假~教育网的用户有福了！

由于目前天-河蟹-朝的G-F-W只监控ipv4网络，因此具有ipv6访问能力的用户——教育网用户以及部分省市的用户（主要是电信）可以通过**ipv6+修改hosts**实现穿越！

那么关键就是hosts文件了.ipv6-hosts（[http://code.google.com/p/ipv6-hosts/](http://code.google.com/p/ipv6-hosts/)）解决了这个问题。


#### ipv6+hosts的优势与不足





	
  * 优势：速度给力！教育网里经常bt的童鞋都知道!

	
  * 不足：可浏览网站极为有限（毕竟现在支持ipv6的大网站十分有限）




### 结论


笔者是以上几种方法综合使用的~我相信通过以上几种方法都可以顺利的实现翻-河蟹-墙的功能~Good luck!

=========================================================================================


本人比较依赖google，但是由于一些大家都知道的原因，大部分google服务在tian朝无法访问。
屏蔽原理是什么？
这种无法访问可能是通过使DNS不解析域名达到的。
该如何解决？
方法一（简单、不稳定）：知道为何无法访问了，我们就可以通过修改本机上的IP hosts，“手动解析”各个google的域名即可访问。当然这只是临时性的办法，因为不知何时这些IP就会不可用。但至少目前是可用的。[注意此方法必须使用https访问]
方法二（稳定，<del>比较复杂或需要资金购买</del>）：可以通过SSH等加密匿名方式访问，但是要确保已经设置好本机的SSH并且已经有了SSH帐号密码(免费的或者付费的)。该种方法的原理，这里就不详述了，学过网络原理的应该都有所了解，若不懂的，请google之。
方法三（临时性）：可以通过在线代理或者寻找免费的代理服务器，代理上网。这种方法很临时，不是长久之计。
你什么时候说关键的？

好吧，不要急，我这就说最关键的部分！



2011-4-26 更新
感谢[80在云](http://www.80ht.cn/)提供信息,[原文地址](http://www.80ht.cn/2011-04-09-zui-xin-google-docs-gu-ge-wen-dang-hosts.htm)

[再次提示:]修改后一定要使用https方式访问

[text]
209.85.225.101 docs.google.com
#209.85.225.102 groups.google.com
74.125.95.83 spreadsheets.google.com
74.125.95.83 spreadsheets0.google.com
74.125.95.83 spreadsheets1.google.com
[/text]

目前我使用的就是这两个，感谢[Tothink博客](http://tothink.net/)提供
原博客上还有很多，但是有些不可用，有需要可以去看看，[地址](http://tothink.net/?p=338)

修改的位置：

[text]
Windows：C:\Windows\System32\drivers\etc\hosts
Linux: /etc/hosts
[/text]

注意修改后要使设置生效需要重启网络
Windows环境：运行中(Win+R键)启动cmd，输入如下命令即可

[text]ipconfig /flushdns[/text]

Linux上要重启一下网络，使设置生效

[bash]sudo /etc/init.d/networking restart[/bash]

Good Luck！
