---
layout: post
title: "Customize Octopress"
date: 2013-03-08 22:27
comments: false
categories: [octopress]
published: true
---

<!-- * Toc -->
<!-- {:toc} -->

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
