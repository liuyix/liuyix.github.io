---
layout: post
title: "百度校招-系统研发工程师-笔试题"
date: 2013-10-15 01:36
comments: true
categories: Life General
---

几道编程算法题：

+ 实现类似wget一样的进度条
+ 100亿个单词，每个单词长度小于30，输出去重后的所有单词。

<!--more-->

### 实现类似wget进度条

> 当时没有想出来，回来才搜索之后才知道考察的是对转义符的理解。

关于换行，话题看起来看似简单，但实际内容不少。

**主流操作系统文本换行的差异**

| OS | 按下回车后插入的控制字符 | 含义 |
| --
| Windows | `\r\n` | 0x0D 0x0A *CR LF* 
| Linux | `\n` | 0x0D *LF* 
| Mac OSX | `\r` | 0x0D *CR* 

因此你经常会遇到Windows下用notepad看某些Linux编辑的文本，都没有换行。

基本的内容就这么多，如何实现wget的进度条即是在Linux下用`\r`而不用`\n`，这样会不断的将新内容输出到同一行，从而达到“刷新”的效果。


{% codeblock lang:c  demo.c %}
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

//类似wget的进度条的实现，实际就是转移符\r的使用，\r的作用是返回至行首而不换行
int main(int argc, char *argv[])
{
    unsigned len = 60;
    char *bar = (char *)malloc(sizeof(char) * (len + 1));
    for (int i = 0; i < len + 1; ++i)
    {
        bar[i] = '#';
    }
    for (int i = 0; i < len; ++i)
    {
        printf("progress:[%s]%d%%\r", bar+len-i, i+1);
        fflush(stdout);//一定要fflush，否则不会会因为缓冲无法定时输出。
        usleep(100000);// 睡眠100ms
        //sleep(1);
    }
    printf("\n");
    return 0;
}

{% endcodeblock %}


### 给定100亿个单词，每个单词长度小于30，输出去重后的所有单词序列。

面试准备不充分，这是trie树的最典型的题目了。
更多的信息可以看July的文章。
http://blog.csdn.net/v_july_v/article/details/6897097

