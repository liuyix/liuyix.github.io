---
layout: post
title: "git workflow"
date: 2015-04-05 23:30
comments: true
categories: Coding
---

Git近几年有逐渐取代svn的趋势，一部分原因是github的风靡，google code也关门大吉，令人唏嘘[^1]。很多公司开始逐渐从svn代码仓库迁移到企业私有版的github--[gitlab](https://gitlab.com/)。知道怎么玩git是大势所趋。

Git小白推荐读物：atlassian出版的[Git Tutorials](https://www.atlassian.com/git/tutorials)，这家公司拥有mac上最佳git客户端SourceTree以及Bitbucket。

本文是对[Comparing Workflows](https://www.atlassian.com/git/tutorials/comparing-workflows)这篇文章和自己的使用心得所做的总结。

以下三种工作流只是典型的代表，不是规范，而是参考，可以结合自己的使用特点灵活选择和修改。

- Centralized Workflow
- Feature Branch Workflow
- Gitflow

<!--more-->

### Centralized Workflow

- 适合几个人的小项目或者自己玩。
- 和svn差别小。
- 多人协作采用rebase方式并入master。
    - 小李和小红分别把代码拉到本地进行开发，然后小李先提交到了master，这时候小红再提交她的修改会被reject，因为push的过程中小红本地的Master分支和remote（服务器）上的不同。这时候小红需要`git pull --rebase origin master`将远程的代码和她本地的修改进行融合，融合的目的是让小红提交的所有的commit看起来实在小李同学push到master分支后的那个点开始做的。

![小红在小李之后push到master](https://www.atlassian.com/git/images/tutorials/collaborating/comparing-workflows/centralized-workflow/11.svg)

### Feature Branch Workflow

- 适合几个人的小项目。
- 利用*pull request*进行code review和交流改进。

相比*Centralized Workflow*，这个工作流没有增加多少内容，只是在merge过程时一定要创建`pull request`让大家可以有个代码review和交流修改的过程。

### Gitflow

比较适合多人的大型项目。

![git branching model](http://nvie.com/img/git-model@2x.png "git branching model")

- master
- develop
- release
- feature
- bugfix

<!-- 一个例子是线上生产稳定的跑着1.2版本（master分支），开发和测试主要活跃在develop分支，产品路线图中计划的下个月的1.3版本的发布是develop的一个release分支。在1.3版本中总共加入了3个feature和5个bugfix，总共由4个人负责代码开发。-->

<!--2个主要分支：master和develop。master分支对应生产环境跑的代码，很像rpm包的`current channel`；develop对应的就是rpm发布的`test channel`，feature和release在完成后都会并入到develop分支。-->

### More Readings 

- [Google's vs Facebook's Trunk Based Development](http://paulhammant.com/2014/01/08/googles-vs-facebooks-trunk-based-development/)


[^1]: http://google-opensource.blogspot.com/2015/03/farewell-to-google-code.html