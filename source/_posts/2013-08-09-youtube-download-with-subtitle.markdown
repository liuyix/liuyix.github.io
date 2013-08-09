---
layout: post
title: "翻墙下载附带字幕的youtube视频"
date: 2013-08-09 23:59
comments: true
categories: 
---

> 许久没写了，上一篇水文教程。   

需要的工具：

+ [goagent](https://code.google.com/p/goagent/)
+ [youtube-dl](http://rg3.github.io/youtube-dl/download.html)

goagent教程就不上了，这个是翻墙的基本知识。:-P

### 使用youtube-dl下载youtube视频

事先声明, Windows平台的我没有试过。按照说明需要安装python 2.6以上的版本才能运行。  
然后先用浏览器翻墙看一下复制你要下载的youtube的链接，比如 [http://www.youtube.com/watch?v=9bZkp7q19f0](http://www.youtube.com/watch?v=9bZkp7q19f0)  
然后进入命令行，输入

1. 此步骤可选，若想选择下载的格式和大小，则可以先列出可下载的格式列表，使用命令： `./youtube-dl --write-sub --proxy 'http://127.0.0.1:8087' --list-formats http://www.youtube.com/watch?v=OPethpwuYEk`
1. 若执行了(1)则此步骤中可以指定`--format 22`, 即`./youtube-dl --write-sub --proxy 'http://127.0.0.1:8087' --format 22 http://www.youtube.com/watch?v=OPethpwuYEk`

几分钟之后就会下载好选择的视频(文件名称默认为解析出的视频名称)

-------

让我的感觉印象深刻的是这个项目是由python编写，但是项目的部署非常不错，只有一个可执行文件，没有任何其他依赖。这个之后研究下 :-)
