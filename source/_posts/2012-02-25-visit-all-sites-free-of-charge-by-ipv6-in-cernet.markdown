---
comments: true
published: true
date: 2012-02-25 15:40:12
layout: post
slug: visit-all-sites-free-of-charge-by-ipv6-in-cernet
title: 教育网中使用ipv6免流量访问*所有*网站（包括所有被QIANG网站）——NAT64/DNS64设置指南
wordpress_id: 548
categories:
- General
tags:
- gfw
- howto
---

感谢强大的ipv6!


> 使用纯IPv6网络的用户如果需要访问IPv4的网络资源时，一般需要通过第三方软件来实现，而现在大家可直接通过支持**NAT64/DNS64**的服务器，来实现IPv6与IPv4之间的NAT,从而实现IPv6网络访问IPv4资源。




目前互联网上公布的二台DNS64服务器地址为：

```
2001:778::37
2001:df8:0:7::1
```



通过简单设置就可以实现利用ipv6访问**所有网站**。
<!-- more -->


## 一些限制





	
  1. 目前该方法不能在**windows xp**上使用，只能在windows vista、windows 7上使用。

	
  2. 只能使用基本web服务，浏览网页，其他如登录QQ客户端不行（使用网页QQ可以）。




## 设置方法




### Windows7设置


进入网络和共享中心，点击本地连接，设置属性，双击ipv6属性输入上面的两个DNS服务器地址。同时取消ipv4协议以达到纯ipv6上网，最后点击确定就大功告成！


### Ubuntu设置


对Linux了解的不多，采取的方法也许不是最佳的。Ubuntu网络管理程序使用的是NetworkManager，这个工具说实话很垃圾。无法设置很多选项，比如说我们即将设置的nameserver，而且每次联网都会覆盖掉你自定义的设置。

牢骚到此为止。

设置过程：



	
  1. 首先打开NetworkManager，**编辑连接**-->"**你目前用的网络连接"**-->"ipv4标签下选择**禁用**"-->**ipv6标签，选择自动**

	
  2. 编辑`/etc/resolv.conf`

```bash

sudo gedit /etc/resolv.conf`

```

添加如下内容：

    
    nameserver 2001:778::37
    nameserver 2001:df8:0:7::1






	
  * 设置好resolve.conf之后，每次重启网络或者重新联网时NetworkManager都会覆盖掉你的设置，这里有个下下策的解决办法，运行下面的命令

    
    sudo chattr +i /etc/resolv.conf


这样resolv.conf就变成无法修改了。可以避免被覆盖。如果要想恢复，则运行

    
    sudo chattr -i /etc/resolv.conf







## 使用感受


最近这几周一直在使用纯ipv6利用该方法上网。总得来说，还凑合。优点很明显，所有网站通行无阻。缺点就是_速度慢_，**不稳定——偶尔会抽风。**

建议是将此方法结合着ipv6 hosts方法达到更好的使用体验。


## 参考链接





	
  * [在IPv6网络下访问IPv4资源的方法(利用NAT64/DNS64实现)](http://www.ipv6bbs.cn/archiver/tid-152.html) via [IPv6论坛](http://www.ipv6bbs.cn/)


