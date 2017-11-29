---
layout: post
title: "高效Jenkins用户的第3个习惯"
date: 2016-05-23 20:54:36 -0700
comments: true
categories: Jenkins Continuous-Integration 中文
---

本文内容部分来源于**Andrew Bayer**发布在SlideShare上的 [*7 habits of highly productive Jenkins Users (2014 Edition)*](http://www.slideshare.net/andrewbayer/seven-habits-of-highly-effective-jenkins-users-2014-edition).

# 习惯 3: 让Jenkins任务自动化 #

## 1. Script Console 和 Scriptler 插件##

使用(Scriptler插件)[https://wiki.jenkins-ci.org/display/JENKINS/Scriptler+Plugin]，保存和重用Groovy脚本

## 2. 一些Scriptler可以做的事情的例子

* 通过匹配，控制一些job的开关 (enable, disable)
* 清除build queue
* 为所有的jobs设置log rotation/discard old builds等等配置参数：如果采用手工的方法，需要分别对每一个job进行配置，步骤繁琐
* 对所有的jobs设置取消夜晚时间的SCM Polling: 这个功能其实就是批量设置jobs schedule
* 对所有jobs执行log rotator

这只是一些例子。可以看出，使用scriptler可以方便对job的配置进行批量操作

<!--more--> 

## 3. System Groovy build steps

* Groovy build steps 是在build中去执行system Groovy的脚本。需要注意的是，要保证Jenkins有权限执行build的全过程。
* 利用Groovy build steps, 可以方便地做一些类似于plugin的功能，或者作为在开发一个plugin之前的测试
* 通过Scriptler scripts, 可以在多个builds中重用系统脚本

## 4. 自动生成Jenkins jobs

* 使用Jenkins REST API 和 CLI，可以创建新的job或者改变已有的job
* 可以使用DSL来定义job甚至包含多个job的workflow

## 5. 一些支持DSL的Plugin

* [Job DSL plugin](https://wiki.jenkins-ci.org/display/JENKINS/Job+DSL+Plugin)
* [DotCI plugin](https://wiki.jenkins-ci.org/display/JENKINS/DotCi+Plugin)
* [Workflow plugin (Pipeline plugin)](https://wiki.jenkins-ci.org/display/JENKINS/Pipeline+Plugin)

**阅读同主题内容**

- [高效Jenkins用户的第1个习惯](http://euccas.github.io/blog/20151210/jenkins-user-habits-1.html)
- [高效Jenkins用户的第2个习惯](http://euccas.github.io/blog/20151215/jenkins-user-habits-2.html)
- [高效Jenkins用户的第3个习惯](http://euccas.github.io/blog/20160523/jenkins-user-habits-3.html)
- [高效Jenkins用户的第4个习惯](http://euccas.github.io/blog/20161010/jenkins-user-habits-4.html)
- [高效Jenkins用户的第5个习惯](http://euccas.github.io/blog/20161216/jenkins-user-habits-5.html)