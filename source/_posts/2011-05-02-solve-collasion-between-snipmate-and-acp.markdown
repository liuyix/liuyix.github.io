---
comments: true
published: false
date: 2011-05-02 12:29:13
layout: post
slug: solve-collasion-between-snipmate-and-acp
title: snipMate(snipMate.vim)与AutoComplPop(acp.vim)冲突的解决方法
wordpress_id: 248
categories:
- Techs
- 未分类
tags:
- vim
- 解决方法
---

今天开始熟悉vim上的开发，没想到一下子就遇到了一个问题——snipMate与AutoComplPop(以下简称acp)的冲突问题，具体症状为输入while或者for等关键词时会自动跳出补全窗口，按在菜单中来回选择而不是snippets。
解决办法：<!-- more -->



	
  1. 在snipMate.vim中添加以下代码：
[text]
fun! GetSnipsInCurrentScope()
let snips = {}
for scope in [bufnr('%')] + split(&amp;ft, '\.') + ['_']
call extend(snips, get(s:snippets, scope, {}), 'keep')
call extend(snips, get(s:multi_snips, scope, {}), 'keep')
endfor
return snips
endf
[/text]

	
  2. 在.vimrc中添加以下的设置[text]let g:acp_behaviorSnipmateLength=1[/text]


这样就把snipMate集成到了acp中，可以通过**输入大写的关键词(FOR,WHILE...)从弹出的菜单中选择**。
