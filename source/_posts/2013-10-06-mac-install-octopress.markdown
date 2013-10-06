---
layout: post
title: "mac上安装octopress"
date: 2013-10-06 12:31
comments: true
categories: mac
---

> Update: 经人提醒，可以改用国内淘宝的rubygems源下载，具体操作：http://ruby.taobao.org/   
> ~~可算折腾出来了。最大的障碍是渣一样的网络，rubygems想法不错，可到了国内情况就会变得很糟糕。最后不得已用goagent总算顺利的完成了。~~

1. 安装homebrew
1. 安装rbenv以及ruby-build
1. `rbenv install 1.9.3-p448`
1. `official install octopress`
1. 在octopress目录下面新建配置文件`echo '1.9.3-p448' > $your-octopress-path/.ruby-version`

### 原有的octopress迁移到mac

如果之前在其他地方已经使用了octopress，那么在mac上的稍有不同。具体为：

+ clone *yourname.github.com*的source分支：`git clone git clone -b source git@github.com:yourname/yourname.github.com.git octopress`
+ 在clone*yourname.github.com*的master分支到`$your_octopress/_deploy`目录: `git clone git clone git@github.com:yourname/yourname.github.com.git _deploy`

```bash

# 如果之前就已经在使用octopress，迁移到mac的话，不要clone octopress源，而是要clone你自己的repo源的source分支
git clone -b source git@github.com:yourname/yourname.github.com.git octopress
git clone git@github.com:yourname/yourname.github.com.git octopress/_deploy

###### 安装octopress ######
# install homebrew
ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"

# 使用brew安装rbenv
brew install rbenv ruby-build

# 修改.bash_profile
echo 'export RBENV_ROOT=/usr/local/var/rbenv' >> ~/.bash_profile
echo 'if which rbenv > /dev/null; then eval "$(rbenv init -)"; fi' >> ~/.bash_profile

# 关闭terminal，再重新开启
rbenv install ruby-1.9.3-p448
rbenv versions #应该显示的是system和1.9.3-p448

# 进入到你的octopress
cd $your-octopress
echo '1.9.3-p448' > .ruby-version

# 再次关闭终端，重新打开进入到你的ocotpress目录
ruby --version # 应该显示的是ruby 1.9.3p448

# 推荐可选操作：更改rubygems源至国内淘宝源，下载更稳定,参考链接：ruby.taobao.org
gem sources -l # 看一下默认的rubygems源的url
gem sources --remove https://rubygems.org/ #此处的url以上一条命令为准，有时可能是http而不是https
gem sources -a http://ruby.taobao.org
gem sources -l # 此处应该只显示的是淘宝的rubygems源

# 现在就可以参考官方的安装说明安装了
gem install bundler
rbenv rehash    # If you use rbenv, rehash to be able to run the bundle command
bundle install

# 如果是第一次安装octopress，还需要安装默认的theme
rake install

```
