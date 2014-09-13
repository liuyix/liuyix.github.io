---
layout: post
title: "SMP L1 Cache MESI Coherence Protocol Internal"
date: 2014-01-07 15:02
published: true
comments: true
categories: Research
---

## Gem5 Simulator Ruby Memory System

Ruby Memory

## 基于Directory的SMP L1 Cache MESI协议的内部实现

**Directory** :
**SMP** :
**L1** :

![/images/Diagrama_MESI.gif](/images/Diagrama_MESI.gif)

而实际上**SMP架构**中的MESI具有多个*瞬时状态* ,在研究Gem5模拟器中集成的_Ruby Memory System Simulator_的实现，根据协议实现代码，我得到了以下添加了瞬时状态后的有限状态机图示（ **该图依然为简化后的图，其中省略了自旋状态转换** ，这样看起来更清晰些）


![MESI](/images/MESI-orig.png)

当然这依然不是最终实现的结构，该图并没有考虑目前已经广泛应用在各种处理器上的 _Prefetcher_ 
本文之后会介绍这些 _State_ 以及对应的 _Event_ 。
