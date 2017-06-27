---
layout: post
title: "高效Jenkins用户的第4个习惯"
date: 2016-10-10 20:32:01 -0800
comments: true
categories: Jenkins Chinese 中文
---

本文内容部分来源于**Andrew Bayer**发布在SlideShare上的 [*7 habits of highly productive Jenkins Users (2014 Edition)*](http://www.slideshare.net/andrewbayer/seven-habits-of-highly-effective-jenkins-users-2014-edition).


# 习惯 4: 精选你所使用的Jenkins功能插件(Plugin)

当你使用了越来越多的Jenkins功能插件时，就需要花一些时间和精力来维护和清理所有的功能插件。 因为当你安装了太多的Jenkins插件时，有可能会带来一些不好的效果，诸如减慢系统速度，占用多过资源，产生无效的记录文件等等。为了避免使用过多的Jenkins插件造成的各种问题，你应该注意下面几个方面。

## 1. 只安装你真正需要的功能插件 ##

在安装一个功能插件之前，你都应该问一个问题：我真的需要这个插件吗？

如果你并不打算真正使用一个插件，就不要安装在Jenkins Master上。

不同的插件可能包含有一些类似的功能，你所需要完成的事情，也不仅仅只有一个插件可以实现。这时就需要在一些功能类似的插件中选择你真正所需的。

功能插件可能会给Jenkins service的稳定性造成预期之外的影响，并且可能增加系统的负载和每一个job运行的时间。充分考虑到这些可能的负作用，尽量避免安装你并不是真正需要的插件。

<!--more--> 

## 2. 清理旧的插件和数据 ##

定期检查和删除你不再使用的Jenkins功能插件。

在Jenkins管理页面 (Manage Jenkins) 中，注意关于old data的描述。当你删除一个Jenkins插件后，要把有关的历史数据也同时删除。

及时删除不需要的数据，可以加速Jenkins Master启动时加载配置和所有jobs的过程。


## 3. 建立你的必备插件列表 ##

根据你的使用需求和经验，选择你所需要的Jenkins功能插件。这些功能插件应该是满足你所需要的功能，并且性能良好稳定。为你的这些插件建立一个列表并且维护它。


**Andrew Bayer**推荐了一些他所使用的Jenkins功能插件。所有这些提供的插件都可以通过Jenkins插件管理功能(Manage Plugins)来查找和安装。

- **Job Config History**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/JobConfigHistory+Plugin) 
  - 功能：保存job configuration的历史，记录每一次改动的信息。对于job configuration每一次的改变，保存一个config.xml文件。提供overview页面，方便查看全部的改变。可以对比查看两次改动之间的区别。
  
- **Static Analysis Plugins**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/Static+Code+Analysis+Plug-ins)
  - 功能：处理各种静态代码分析结果数据，生成可视化报告（包括趋势图，Build Summary，结果汇总分析等等）

- **xUnit**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/xUnit+Plugin)
  - 功能：生成和发布单元测试报告。可以把各种测试结果转化为jnit格式。

- **Parameterized Trigger**
  
  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/Parameterized+Trigger+Plugin)
  - 功能：参数化配置trigger build. 对于一个build job，可以定义多个配置，用于不同的条件和参数。

- **Conditional Build Step**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/Conditional+BuildStep+Plugin)
  - 功能：可以灵活配置的build step。通常和Parameterized Trigger配合使用。

- **Tool Environment**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/Tool+Environment+Plugin)
  - 功能：让你可以自定义使用Jenkin tool的自动安装。在一个job的执行过程中安装指定的tools，供这个job使用。

- **EnvInject**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/EnvInject+Plugin)
  - 功能：帮助你管理环境变量，包括删除Jenkins Java process引入的一些环境变量，在一个node启动时设置所需的环境变量，设置密码值等等。

- **Rebuild**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/Rebuild+Plugin)
  - 功能：可以rerun每一个被执行过的parameterized build，保存了parameterized build每一次使用的参数，并且允许你在执行rebuild时修改这些参数。
 
- **Build Timeout**

  - [插件介绍](https://wiki.jenkins-ci.org/display/JENKINS/Build-timeout+Plugin)
  - 功能：设置build的时间限制，当一个build时间超过预设时，会自动被停止。这个插件不能用于Jenkins pipelines.

**阅读同主题内容**

- [高效Jenkins用户的第1个习惯](http://euccas.github.io/blog/20151210/jenkins-user-habits-1.html)
- [高效Jenkins用户的第2个习惯](http://euccas.github.io/blog/20151215/jenkins-user-habits-2.html)
- [高效Jenkins用户的第3个习惯](http://euccas.github.io/blog/20160523/jenkins-user-habits-3.html)
- [高效Jenkins用户的第4个习惯](http://euccas.github.io/blog/20161010/jenkins-user-habits-4.html)
- [高效Jenkins用户的第5个习惯](http://euccas.github.io/blog/20161216/jenkins-user-habits-5.html)