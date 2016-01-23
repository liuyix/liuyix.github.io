---
layout: post
title: "MySQL物理热备份xtrabackup特性"
date: 2016-01-09 17:41
comments: true
categories: MySQL
---

截至目前2016年01月, xtrabackup有1.x和2.x可供下载使用。[Release Note](https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes.html)

- 1.x中的最后版本1.6.7,最后更新时间是2012年12月20日[^1]
- 2.x系列是目前主力系列
    + 【推荐】稳定版分支是2.2系列，最新稳定版本是2.2.13，最后更新时间为2015年10月22日[^2]。
    + 2.3系列刚刚推出GA版本（），按照习惯不是很推荐在生产环境使用。
    + 【过时】2.1系列最后版本是2.1.9，最后更新时间是2014年5月7日[^3]。
    + 【过时】2.0系列最后版本是2.0.8，最后更新时间是2013年9月13日[^4]


## 各版本的特性介绍

以下介绍xtrabackup 2.1到2.3版本的新增特性。


### 2.1系列

新特性

- 支持 Compact Backups
- 支持 Encrypted Backups

重大变化

- 使用Perl的*DBD::MySQL*取代之前的mysql命令行方式
- **不再支持 InnoDB 5.0 and InnoDB 5.1 builtin** 
- `--remote-host `不再支持

### 2.2系列

新特性



[^1]: [https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/1.6/1.6.7.html](https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/1.6/1.6.7.html)
[^2]: [https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/2.2/2.2.13.html](https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/2.2/2.2.13.html)
[^3]: [https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/2.1/2.1.9.html](https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/2.1/2.1.9.html)
[^4]: [https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/2.0/2.0.8.html](https://www.percona.com/doc/percona-xtrabackup/2.3/release-notes/2.0/2.0.8.html)


