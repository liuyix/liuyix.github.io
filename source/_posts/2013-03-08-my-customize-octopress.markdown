---
layout: post
title: "Octopress修改记录"
date: 2013-03-08 22:27
comments: false
categories: [octopress]
published: true
---

<--more-->

### Octopress

Reference: [Clone Your Octopress to Blog From Two Places](http://blog.zerosharp.com/clone-your-octopress-to-blog-from-two-places/)

`$octopress` 代表的是 `git clone -b source git@github.com:username/username.github.com.git octopress`

octopress有2个branch—— `source` 和 `master`   

`master` 是jekyll生成后的静态网站源码，**位置在_deploy目录**  
`source` 是 octopress源码，是*octopress*根目录   



#### Blog流程

`cd $octopress && rake generate`

1. 更新octopress源码(目的是要保存markdown源文件)
    + `git add <modified file>`
    + `git commit -am 'some comment'`
    + git push origin **source**
2. 生成后的网站源码部署
    + `rake deploy`
    
### 多个电脑上编写octopress博客

可能很多人会像我一样有这样的需求：工作地点和家里都想要更新下自己的blog，还有有时会在自己的台式机和笔记本上更新blog，这时你就会遇到我现在的问题： *怎么在多个电脑上部署octopress环境*


### 表格boarder的修复

参考: [链接]('http://programus.github.com/blog/2012/03/07/add-table-data-css-for-octopress/')  
只是作者修改的有点麻烦，我只是把data-table.css粘贴到了 `sass/custom/_styles.scss` 里面了就出效果了。

### markdown interpreter换成了kramdown

因为默认的不支持footnote，所以直接换成了[kramdown]

#### Update 2013-07-14

octopress升级到了2.0, 新的`rdiscount`支持了footnote特性，因此又换回了`rdiscount`


### 404 page

在source下面建立404.html

### 自定义sidebar

这个教程里就有

### category-list

TODO

### stylesheet小幅改动

#### awkward ul ol

[issue417](https://github.com/imathis/octopress/issues/417)
在 `sass/custom/_styles.scss` 里修改

#### footnote
一个插件[octopress-footnote](https://github.com/fmcypriano/footnote-octopress),只是个人试用效果不好，遂将js部分去掉了，配合  [kramdown] 正好适合


[kramdown]: http://kramdown.rubyforge.org
