---
layout: post
title: "高效Jenkins用户的第1个习惯"
date: 2015-12-10 19:32:57 -0800
comments: true
categories: jenkins Chinese 中文
---

本文内容部分来源于**Andrew Bayer**发布在SlideShare上的 [*7 habits of highly productive Jenkins Users (2014 Edition)*](http://www.slideshare.net/andrewbayer/seven-habits-of-highly-effective-jenkins-users-2014-edition).

# 习惯 1: 保持Jenkins Master的稳定与可恢复

## 1. 使用LTS Release ##

LTS release每12周发布一个新版本

LTS release版本发布都会保证通过自动化的acceptance testing和手工testing matrix

## 2.不要急于升级plugins，保持谨慎 ##

plugin的升级可能包含非常多的变化

不是所有的升级都会保证向前兼容。比如最近Extended Email Plugin的升级，就造成之前的recipient/trigger配置不可用

新功能也许不稳定

<!--more--> 

## 3. 对升级进行测试 ##

建议在测试环境中对升级和新的plugin进行测试，之后再进行production环境的升级

建立针对plugin功能的测试

在更大的规模进行测试

大的改变需要至少经过几天的测试

## 4. 备份Jenkins Configuration ##

建议使用[thinBackup plugin](https://wiki.jenkins-ci.org/display/JENKINS/thinBackup)

可以通过对$JENKINS_HOME做整体备份实现有效的备份，缺点是速度慢和占用较多的存储空间

Jenkins支持仅仅备份config files，而不需要备份所有的builds。参考[这个gist](https://gist.github.com/abayer/527063a4519f205efc74)中的代码实现这一功能。

## 5. 避免使用Maven job类型 ##

Maven plugin中的Mavin job type可能存在一些问题，包括plugin support, lazy loading等等

在大规模应用中可能会引起一些意外的问题，不建议使用

## 一些解释 ##

### 什么是LTS Release? ###

Jenkins LTS Release: Jenkins Long-Term Support release. 类似于Ubuntu的LTS版本。

具体说明[在这里](https://wiki.jenkins-ci.org/display/JENKINS/LTS+Release+Line)。

### 关于Jenkins Maven Jobs ###

在Jenkins中可以通过两种方式build Maven project

1. 使用一个 free-style project 和 Maven build step

2. 使用一个 Maven-style project (配置job type为Mavin job type)
推荐使用第一种方法，因为第二种方式可能会出现问题

**阅读同主题内容**

- [高效Jenkins用户的第1个习惯](http://euccas.github.io/blog/20151210/jenkins-user-habits-1.html)
- [高效Jenkins用户的第2个习惯](http://euccas.github.io/blog/20151215/jenkins-user-habits-2.html)
- [高效Jenkins用户的第3个习惯](http://euccas.github.io/blog/20160523/jenkins-user-habits-3.html)
- [高效Jenkins用户的第4个习惯](http://euccas.github.io/blog/20161010/jenkins-user-habits-4.html)
- [高效Jenkins用户的第5个习惯](http://euccas.github.io/blog/20161216/jenkins-user-habits-5.html)
