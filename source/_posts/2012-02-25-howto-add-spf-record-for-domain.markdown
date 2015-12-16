---
comments: true
published: true
date: 2012-02-25 16:26:17
layout: post
slug: howto-add-spf-record-for-domain
title: 域名邮件不再被spam——SPF记录设置
wordpress_id: 360
categories:
- General
tags:
- howto
---

一直使用的是QQ提供的[域名邮箱](http://domain.mail.qq.com/)功能，很不错。本文旨在教你如何设置SPF记录防止自己域名的邮件被标记为spam。


## 什么是SPF记录


参考wiki：[http://en.wikipedia.org/wiki/Sender_Policy_Framework](http://en.wikipedia.org/wiki/Sender_Policy_Framework)

SPF是**Sender Policy Framework**的简称，是一种email验证系统，旨在通过检测email proofing，验证发送者IP地址的方法来杜绝垃圾邮件的方法。


> 接收邮件方会首先检查域名的SPF记录，来确定发件人的IP地址是否被包含在SPF记录里面，如果在，就认为是一封正确的邮件，否则会认为是一封伪造的邮件进行退回。




## 设置过程


本文以DNSPod为例展示QQ域名邮箱的SPF设置过程。



	
  1. 进入DNSPod制定域名的管理界面

	
  2. “添加记录”，填入如下内容：

    
    v=spf1 include:spf.mail.qq.com ~all


  3. 最后点击保存即可


