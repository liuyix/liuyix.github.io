---
layout: post
title: "docopt -- Python必备的命令行接口模块"
date: 2015-10-21 00:02
comments: true
categories: Python, Develop
---


docopt很适合经常需要用python写命令行工具的同学使用。

## docopt之前

工作需要，经常会用大块的代码来定(ren)义(rou)命令行界面的工具。代码经常是如下的样子：

```python

import optparse

parser = optparse.OptionParser()
parser.add_option('--foo', '-f', default='1', type='int')
parser.add_option('--bar', '-b', action='store_true')
# 类似以上的代码大概几十行

opts, args = parser.parse_args()

```

每一个python脚本都需要提供类似的接口。因此每一次都需要写类似的代码。在写过几次后为了保持DRY原则，我将初始化parser封装为一个method放在util部分。可是依旧是逃不过重复的写`parser.add_option`。不止一次地我考虑干脆自己写个模板类，以后命令行的定义直接以配置文件的形式写出来，然后每次都通过读取这个配置文件自动化的去生成parser。我相信这个问题我一定不是第一个遇到，应该会有已知的模块解决这个laber intensive的工作。

正在这个时候，偶然看到Python weekly发现了docopt

## docopt

docopt官网地址：http://docopt.org/

docopt的作者有一个30分钟的视频很好的介绍了docopt这个moudule。推荐大家看一下，自备梯子~ [https://youtu.be/pXhcPJK5cMc](https://youtu.be/pXhcPJK5cMc)

更令懒人们惊喜的是作者还制作了一个js版本的docopt，可以让你在浏览器中把玩docopt： http://try.docopt.org/

使用docopt后，代码上会更加Pythonic，具有很高的可读性，命令行接口的定义所见即所得的样式：

```
#docopt example

mydoc = """Naval Fate.

Usage:
  naval_fate.py ship new <name>...
  naval_fate.py ship <name> move <x> <y> [--speed=<kn>]
  naval_fate.py ship shoot <x> <y>
  naval_fate.py mine (set|remove) <x> <y> [--moored|--drifting]
  naval_fate.py -h | --help
  naval_fate.py --version

Options:
  -h --help     Show this screen.
  --version     Show version.
  --speed=<kn>  Speed in knots [default: 10].
  --moored      Moored (anchored) mine.
  --drifting    Drifting mine.
"""

from docopt import docopt

arguments = docopt(mydoc, version='0.1')

print arguments
```

这样就定义了一个丰富的命令行接口。命令行接口提供了`--help`和`--version`两个基础功能。其中`--help`输出`mydoc`，`--version`输出指定的`version`信息。

接口还提供了2个参数（ship, mine），每种参数还提供了不同的几种参数的组合。其中`[...]`内是可选参数，`(...|...)`是互斥参数。

