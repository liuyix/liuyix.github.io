---
layout: post
title: "由互联网中的Python应用想到的网站架构的优化"
date: 2015-04-08 22:56
comments: true
categories: Coding,
---

- 国内[^1]
    - 知乎
    - 豆瓣
    - 果壳网
- 国外，只列出我认识的比较出名的，还有好多[^2]=。=
	- Quora 国外的知乎？
	- Dropbox 国外的金山快盘？
	- Disqus 国外的多说？
	- Pinterest 国外的花瓣？
	- Youtube 国外的优酷？
	- Slideshare 国外的百度文库？
	- reddit 国外的猫扑？
	- Yelp 国外的大众点评
	- ...

更多的信息可以参考Python官网的[Python Success Stories](https://www.python.org/about/success/)。

### Quora

下面是QuorWhy did Quora choose Python for its development?a创始人在Quora上对*Why did Quora choose Python for its development?*的回答[^3]

> We decided that Python was fast enough for most of what we need to do (since we push our performance-critical code to backend servers written in C++ whenever possible). As far as typechecking, we ended up writing very thorough unit tests which are worth writing anyway, and achieve most of the same goals.

可以看到对于Python的性能短板，Quora在performance-critical的地方尽可能换用了C++。对于Python没有静态类型，Quora用尽可能的单元测试来确保质量。之所以选择Python其实很大的原因是Founder对Python比较擅长。
进一步google了下，他们的框架用的Pylon。

### 知乎的技术架构

知乎CTO在去年年底有过分享，目前在InfoQ上能找到整理稿。链接：http://www.infoq.com/cn/news/2014/12/zhihu-architecture-evolution 

简而言之用的tornado，自己开发了日志系统Kids，消息传递系统Sink，还有页面渲染ZhihuNode。

### 网站架构及性能的思考

本周听了一次FB周海平在阿里内部的一次分享。无论是阿里、Facebook还是豆瓣，我发现了在网站架构上这几家有很多共同点的：

- MySQL作为存储后端
- MySQL上一定有memcache、tair这样的KV系统做缓存
- 都各自开发了适合自己的消息分发系统，Notify, Thrift, Beanstalkd
- 后端应该都具有实时日志数据分析： HBase、云梯2、Kids
- 不同程度上用异步化来提高性能，并会一直以此来作为性能提升的方法。
- 消息链路上的优化：一个网页的渲染上是树状结构的获取数据，因此可以在通过优化这棵树来达到优化整个过程的目的

### 其他

网站选型不单纯是比较语言优劣，还和社区的发展趋势活跃(谁都不想用过一门可能几年就无人问津的语言)、团队内普遍的好恶和掌控能力（C、C++最好，但是大家都不会）、整个行业的形势（团队内都用Lisp，但是招不到人）等等多种因素有关系。
选择哪门语言确实重要，这决定了未来几年或者更远的时间内技术的发展路线，更重要的当规模扩大后需要在性能优化上要付出的代价。（这里面可以拿Facebook优化PHP作为反例，若是当初扎克用的是java或者c++，也许也不会因此如此兴师动众的重写了PHP生态系统里面的大部分东西。）

[^1]: [知乎-国内使用 Python 作为主要开发语言的知名网站有哪些](http://www.zhihu.com/question/19685768)
[^2]: [Quora-Which Internet companies use Python?](http://www.quora.com/Which-Internet-companies-use-Python)
[^3]: [Quora-Why did Quora choose Python for its development?](http://www.quora.com/Why-did-Quora-choose-Python-for-its-development)