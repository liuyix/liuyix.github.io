---
comments: true
published: false
date: 2011-04-21 09:46:24
layout: post
slug: wordpress-modification
title: Wordpress排版——中文首行缩进和行间距修改的实现
wordpress_id: 186
categories:
- Wordpress
tags:
- wordpress
- 排版
---

Wordpress没有考虑到中文书写的首行缩进的习惯，因此要实现这个功能可以采用修改主题style.css来实现，如果你的主题不常更改的化，这一方法应该说可以一劳永逸。
总体思路：进入Appearance-->Editor-->选择style.css
找到类似

[php]
p {
	padding: 0 0 0.5em;
	line-height:1.5em;
	text-indent: 2em;
}
[/php]

**注意**：不一定是一模一样的，根据主题的不同，一定会有所变化的，但目的都是一样就是找到的<p>的style模板。
找到之后，在大括号("{"和"}"之间)加入`**text-indent: 2em;**`就可以实现首行缩进的功能。要修改行间距就修改`**line-height**`的属性值，1em代表一个字的大小，1.5em表示是1.5倍的行距，修改之后保存即可！

其他的修改排版类的修改同样是这个原理，都是修改style.css中的相关部分。
