---
layout: post
title: "Cache MESI Coherence Protocol Internal"
date: 2014-01-07 15:02
published: false
comments: true
categories: Research
---

## Cache MESI协议的内部实现

> 毕业设计中涉及到对Cache MESI协议的修改，在这里介绍下几乎大多数书本都没有过的介绍的MESI协议内部实现。

一般来讲，MESI协议状态图如下：

![/images/Diagrama_MESI.gif](/images/Diagrama_MESI.gif)

而实际上**多核架构**中的MESI实际具有多个*瞬时状态* ,在研究Gem5模拟器中集成的_Ruby Memory System Simulator_的实现，以下是添加了瞬时状态后的有限状态机图示（ **该图依然为简化后的图，其中省略了自旋状态转换** ，这样看起来更清晰些）

![MESI](/images/MESI-orig.png)

你以为这已经很复杂了对不对？但是这还依旧不是真正实现时的结构，上图忽略了 _Prefetcher_ 。  
本文之后会介绍这些 _State_ 以及对应的 _Event_ 。

```
  enumeration(Event, desc="Cache events") {
    // L1 events
    Load,            desc="Load request from the home processor";
    Ifetch,          desc="I-fetch request from the home processor";
    Store,           desc="Store request from the home processor";

    Inv,           desc="Invalidate request from L2 bank";

    // internal generated request
    L1_Replacement,  desc="L1 Replacement", format="!r";

    // other requests
    Fwd_GETX,   desc="GETX from other processor";
    Fwd_GETS,   desc="GETS from other processor";
    Fwd_GET_INSTR,   desc="GET_INSTR from other processor";

    Data,       desc="Data for processor";
    Data_Exclusive,       desc="Data for processor";
    DataS_fromL1,       desc="data for GETS request, need to unblock directory";
    Data_all_Acks,       desc="Data for processor, all acks";

    Ack,        desc="Ack for processor";
    Ack_all,      desc="Last ack for processor";

    WB_Ack,        desc="Ack for replacement";

    PF_Load,    desc="load request from prefetcher";
    PF_Ifetch,  desc="instruction fetch request from prefetcher";
    PF_Store,   desc="exclusive load request from prefetcher";
  }
  
```



```
// STATES
state_declaration(State, desc="Cache states", default="L1Cache_State_I") {
  // Base states
  NP, AccessPermission:Invalid, desc="Not present in either cache";
  I, AccessPermission:Invalid, desc="a L1 cache entry Idle";
    S, AccessPermission:Read_Only, desc="a L1 cache entry Shared";
    E, AccessPermission:Read_Only, desc="a L1 cache entry Exclusive";
    M, AccessPermission:Read_Write, desc="a L1 cache entry Modified", format="!b";

    // Transient States
    IS, AccessPermission:Busy, desc="L1 idle, issued GETS, have not seen response yet";
    IM, AccessPermission:Busy, desc="L1 idle, issued GETX, have not seen response yet";
    SM, AccessPermission:Read_Only, desc="L1 idle, issued GETX, have not seen response yet";
    IS_I, AccessPermission:Busy, desc="L1 idle, issued GETS, saw Inv before data because directory doesn't block on GETS hit";

    M_I, AccessPermission:Busy, desc="L1 replacing, waiting for ACK";
    SINK_WB_ACK, AccessPermission:Busy, desc="This is to sink WB_Acks from L2";

    // Transient States in which block is being prefetched
    PF_IS, AccessPermission:Busy, desc="Issued GETS, have not seen response yet";
    PF_IM, AccessPermission:Busy, desc="Issued GETX, have not seen response yet";
    PF_SM, AccessPermission:Busy, desc="Issued GETX, received data, waiting for acks";
    PF_IS_I, AccessPermission:Busy, desc="Issued GETs, saw inv before data";
  }
  
```
