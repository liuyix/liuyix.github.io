---
layout: post
title: "python logging模块"
date: 2015-04-05 23:46
comments: true
categories: Python
published: false
---

## Python logging使用


### 多模块使用logging

不要在每个模块里面都创建新的logger，不然会导致重复的log日志输出。只需要在子模块开始：

```
import logging
LOGGER = logging.getLogger('foo module')
LOGGER.setLevel(logging.DEBUG)

....

LOGGER.info('info level logging mesg')
LOGGER.debug('....')
```

在主模块必须要初始化`root`层logging。
python的logging层次化的，最上层的即root的logger初始化可以由`logging.getLogger('')`来拿到然后进行配置。