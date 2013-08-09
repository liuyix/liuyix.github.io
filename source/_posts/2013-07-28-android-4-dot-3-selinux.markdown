---
layout: post
title: "Android 4.3新特性——SElinux简介 "
date: 2013-07-28 00:32
comments: true
categories: android
---

New Jelly Bean -- Android 4.3于7月底发布，这次整体上变化不是很大，所以还是叫Jelly Bean。不过在底层，Android在安全上实际增强了不少，Android 4.3开始集成SELinux, 系统的安全性(*潜力*)提高了一个档次。   

New Jelly Bean, New JB，Android 4.3指的都是Google新发布的Android 4.3系统，代号依旧是Jelly Bean   

## The End of Root? 

**Absolutely NO!!**

1. SELinux 目前（从长远看也很可能）是 *permissive* 模式，即不会拒绝而只是记录*违规*事件；而不是最严格的 *enforce* 模式——只要违反规则就会denial，因为普通消费者能遇到的应用和情形会非常复杂，如果使用该模式会出现更多的问题，同时也会给用户束缚自由的感觉（如同厂商卖给你手机的同时给你规定好了“你只可以xxxx而不能xxxx”，不管你是不是这样觉得，我反正是这么觉得）。这也就意味着使用漏洞提权的方法获得root权限依旧可行，只要SELinux使用的是`permissive`模式。
1. 即使SELinux设置为`enforce`模式，也不会是root的末日。我们还可以通过*线刷*的方法刷入修改的或者其他的定制ROM方法获取Root权限。这样做的前提是手机厂商不锁bootloader（从而给用户自由刷机的权利）。谷歌的Nexus系列就是不锁bootloader——可以使用`fastboot oem unlock` 解锁，之后就可以用`fastboot`随意的修改定制手机ROM。
而三星手机没有强硬的采取严格的手段锁bootloader，可以用Samsung的*官方*刷机工具Odin[^Odin]刷机，一样可以实现不锁bootloader的效果——随意修改定制手机。其他厂商就不太了解了。

#### New challenge for Root

New Jelly Bean给root确实增加一些阻碍，这其中包括：增加了nosuid选项的system分区以及root用户的capabilities的限制。所以两位手机root的大神chainfire和koush在New JB上都采用了新的 *daemon* 模式。

<!--more-->

## SELinux带来了什么？

极大的增强了Android系统的安全性潜力，SELinux机制实际效用依赖于`selinux policy`等SELinux的设定。SELinux的加入为Android进入更高安全性和保密性的团体和企业中提供了很大的便利，Android在企业市场有了更多的想象空间。  
试举一栗子：涉密企业项目的成员移动设备定制化安全服务——可以由Android安全服务公司负责定制ROM，根据项目或者企业需求加入定制化的SELinux策略。好吧，Android移动安全领域的门槛又矮了一截子。

## Android SELinux一窥

Google写的SELinux Guide（[here](https://source.android.com/devices/tech/security/se-linux.html)）对部署和设置SELinux提出了指导性的概括。   
SELinux模块包含了内核空间和用户空间两部分，配置SELinux需要使用相应的Android内核。

### SELinux 编译和部署

1. 下载源代码至`<root>/device/manufacturer/device-name/sepolicy`：  
   + 包含SELinux的内核： https://android.googlesource.com/kernel/common/ 
   + 编译时需要提供的SELinux配置文件: https://android.googlesource.com/platform/external/sepolicy/

2. 修改BoardConfig.mk

```bash

BOARD_SEPOLICY_DIRS := \
        <root>/device/manufacturer/device-name/sepolicy

BOARD_SEPOLICY_UNION := \
        genfs_contexts \ 
        file_contexts \ 
        sepolicy.te 
```

3. 重新编译内核

### SELinux定制流程(via Google)


> + SELinux uses a whitelist approach, meaning it grants special privileges based upon role. Because the default policy provided by Android is so permissive, OEMs have great leeway in strengthening it. Here is how we recommend proceeding:

> + Use the latest Android kernel.
> + Adopt the principle of least privilege.
> + Address only your own additions to Android. The default policy works with the Android Open Source Project codebase automatically.
> + Compartmentalize software components into modules that conduct singular tasks.
> + Create SELinux policies that isolate those tasks from unrelated functions.
> + Put those policies in *.te files (the extension for SELinux policy source files) within the <root>/device/manufacturer/device-name/sepolicy directory.
> + Release your SELinux implementation in permissive mode first.
> + Analyze results and refine policy settings.

## More about SELinux for Android

本节大部分信息都是从[SEAndroid Wiki](http://selinuxproject.org/page/SEAndroid)上获取.

Android 4.3 采用的是SEAndroid[^SEAndroid]，但是做了相当的精简和改变，其中没有以下部分[^1]：

+ SELinux管理API以及附带的示例程序 (The new device admin APIs for managing the SELinux functionality and the SEAdmin sample device admin app for using those APIs.)
+ 除了 `a restricted form of its sefinfo support for labeling apps` 以外，没有任何MAC机制的中间件。
+ 没有 `auditd` ,*也就是说Android 4.3并没有一个收集SELinux审计log的daemon程序* （The audit daemon (auditd) for collecting SELinux audit denials and writing them to /data/misc/audit/audit.log. )
+ 采用和SEAndroid不同的策略，*fully permissive and unconfined* (Our sample policy configuration (Android 4.3 and AOSP master have diverged from our policy, replacing it with a policy that is fully permissive and unconfined).
)
+ 没有重载SELinux策略上的优化，重载策略还需要重启daemon(Some improvements to how policy reloading is handled, particularly avoiding the need to restart daemons.)
+ 对于多用户目录没有合适的安全标签（`security label`)

所以如果想使用*完整版*的SEAndroid需要去下载使用独立的[SEAndroid](https://bitbucket.org/seandroid)

______

未完待续...


[^1]: [http://selinuxproject.org/page/SEAndroid#Merge_Status](http://selinuxproject.org/page/SEAndroid#Merge_Status)
[^SEAndroid]: SELinux项目地址：[https://bitbucket.org/seandroid](https://bitbucket.org/seandroid)
[^Odin]: 有关Odin的XDA论坛地址：[http://forum.xda-developers.com/showthread.php?t=2189539](http://forum.xda-developers.com/showthread.php?t=2189539)
