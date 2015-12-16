---
comments: true
published: false
date: 2012-06-05 19:32:50
layout: post
slug: ipv6-enable-on-websit
title: 内牛满面啊，本博客终于可以ipv6访问了!（ipv6.liuyix.com）
wordpress_id: 661
categories: General

---

博主身在教育网中，登录非大陆的网站是流量计费的，而且每月就是固定的1G流量。（当然BIT是这样的，其他学校可能不是）

于是乎，为了能让本博客生存下去同时保证节省流量，博主不得以尝试了各种支持ipv6的凸墙方法，虽然已经有很多方法可以实现访问国际网站无需流量，但博主依然希望博客可以支持ipv6的直接访问。

机缘巧合之下，知道了[cloudflare](http://www.cloudflare.com/)，于是博主下意识的就搜索"**cloudflare ipv6**"，没想到cloudflare果真已经开始支持ipv6啦！特发此帖以示喜悦之情。

本博客的ipv6地址为：ipv6.liuyix.com 或者是 www.ipv6.liuyix.com

如果你的DNS不支持AAAA信息的话，可以手动添加以下内容至你的hosts文件中

`2400:cb00:2048:1::6ca2:c1c9 ipv6.liuyix.com`

测试了下速度，延时在230ms上下，还算不错。

在这里感谢[cloudflare](http://www.cloudflare.com/)能提供免费的CDN加速以及ipv6的支持。推荐广大的国外主机的博客主使用[cloudflare](http://www.cloudflare.com/)给网站提速。
