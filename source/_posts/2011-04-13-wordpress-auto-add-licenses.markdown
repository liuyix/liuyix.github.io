---
comments: true
published: false
date: 2011-04-13 21:08:17
layout: post
slug: wordpress-auto-add-licenses
title: Wordpress单篇文章尾部自动添加Creative Commons版权信息
wordpress_id: 158
categories:
- Wordpress
tags:
- wordpress
---

通过修改**single.php**实现(如何进入编辑页面？进入wordpress后台，选择Apprearance-->Editor-->右侧边栏中选择single.php)

进入编辑页面后，找到`<?php the_content(); ?>`（注：依各个主题有所不同，你可以通过一些线索来查找，比如正文后的tag链接，正文前的“留评论”链接等），在后面附加上你要添加的版权信息。

建议最好是不用或者使用一些通用的Wordpress函数，参考的blog中在我的主题里，有效的是`<?php the_permalink() ?>`、`<?php the_title(); ?>`、`<?php bloginfo(‘name’);?>`，分别表示的是本文的固定链接、本文的标题以及blog的名称，用这几个PHP变量结合适当的HTML的基本语法就可以做出适合自己的版权声明了

优化代码的原因，我的实际添加过程如下：



	
  * 上传cc版权logo图片到wordpress中

	
  * 嵌入如下代码：
    
    <center><div><img src="http://liuyix.com/wordpress/wp-content/uploads/2012/02/cc-medium.png" alt=""></img><br></br>转载请注明:  | <a href="http://liuyix.com">Liuyix.com</a></div><center>



这样图片是在本地服务器上的，加载起来比链接到creative common网站更快些

你可以从[http://creativecommons.org/choose/](http://creativecommons.org/choose/)中选择适合自己的CC版本，之后会有相应代码生成。

最后不太了解Creative Commons的童鞋，可以看一看[Creative Common的Wiki](http://zh.wikipedia.org/wiki/Creative_Commons)

2012-2-26 Update:

更新到如下的样式：

    
    <center><div>
    <img src="http://liuyix.com/wordpress/wp-content/uploads/2012/02/cc-medium.png"></img><br>转载请注明出处: <input readonly="true" value="<?php the_permalink() ?>" onclick="this.select()"></div><center>
