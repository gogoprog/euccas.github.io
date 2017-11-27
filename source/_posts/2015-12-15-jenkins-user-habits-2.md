---
layout: post
title: "高效Jenkins用户的第2个习惯"
date: 2015-12-15 20:15:38 -0800
comments: true
categories: Jenkins Continuous-Integration Chinese 中文
---

本文内容部分来源于**Andrew Bayer**发布在SlideShare上的 [*7 habits of highly productive Jenkins Users (2014 Edition)*](http://www.slideshare.net/andrewbayer/seven-habits-of-highly-effective-jenkins-users-2014-edition).

# 习惯 2: 大而化小 #

## 1. 使用多个Masters ##

在存在多个project与team的情况下，多个master可以使jenkins jobs的管理更加敏捷和可控

建议根据team, function, access(访问权限) 来划分master

多个master使安装和升级plugin时需要的重启过程变得容易——不需要重启的master不会受到影响

提高系统的稳定性：多个master, 每个master上分配较少数量的jobs，可以使整个系统更为稳定，减少遇到边界情况bug的几率

## 2. 分解jobs

建议在Jenkins中使用模块化和重用，这一点的好处类似于在编程中使用模块化和重用

多job的Build可以方便地在不同的project, release等等中重用

分解job可以避免长时间运行的job在最后阶段出错，导致整个job需要被重新运行：多job的Build可以实现从其中任何一个子job处重新执行

<!--more--> 

## 3. 利用工具帮助分解jobs

混合使用Parameterized trigger, Conditional Build Step, Copy Artifact, Promoted Builds：有效，但是配置困难

Build Pipeline plugin：可以把workflow可视化，集成手工步骤

Workflow plugin: 用DSL定义build steps之间的关系

Jenkins中有许多plugin和有关工具可以实现job分解

### 有关Job分解的Jenkins Plugins ###


#### [Build Pipeline Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Build+Pipeline+Plugin) ####
> This plugin provides a Build Pipeline View of upstream and downstream connected jobs that typically form a build pipeline.  In addition, it offers the ability to define manual triggers for jobs that require intervention prior to execution, e.g. an approval process outside of Jenkins.


#### [Workflow plugin](https://github.com/jenkinsci/workflow-plugin/blob/master/README.md#introduction) ####
> Building continuous delivery pipelines and similarly complex tasks in Jenkins using freestyle projects and traditional plugins can be awkward. You need to mix Parameterized Trigger, Copy Artifact, Promoted Builds, Conditional Build Step, and more just to express what should be a simple script. The Workflow plugin suite attempts to make it possible to directly write that script, what people often call a workflow (sometimes abbreviated flow), while integrating with Jenkins features like slaves and publishers.


#### [Parameterized Trigger plugin](https://wiki.jenkins-ci.org/display/JENKINS/Parameterized+Trigger+Plugin) ####
> This plugin lets you trigger new builds when your build has completed, with various ways of specifying parameters for the new build.
You can add multiple configurations: each has a list of projects to trigger, a condition for when to trigger them (based on the result of the current build), and a parameters section.


#### [Conditional Build Step plugin](https://wiki.jenkins-ci.org/display/JENKINS/Conditional+BuildStep+Plugin) ####
> A buildstep wrapping any number of other buildsteps, controlling their execution based on a defined condition.


#### [Copy Artifact plugin](https://wiki.jenkins-ci.org/display/JENKINS/Copy+Artifact+Plugin) ####
> Adds a build step to copy artifacts from another project. The plugin lets you specify which build to copy artifacts from (e.g. the last successful/stable build, by build number, or by a build parameter). You can also control the copying process by filtering the files being copied, specifying a destination directory within the target project, etc. Click the help icon on each field to learn the details, such as selecting Maven or multiconfiguration projects or using build parameters. You can also copy from the workspace of the latest completed build of the source project, instead of its artifacts. All artifacts copied are automatically fingerprinted for you.


#### [Promoted Builds plugin](https://wiki.jenkins-ci.org/display/JENKINS/Promoted+Builds+Plugin) ####
> This plugin allows you to distinguish good builds from bad builds by introducing the notion of 'promotion'.Put simply, a promoted build is a successful build that passed additional criteria (such as more comprehensive tests that are set up as downstream jobs.) The typical situation in which you use promotion is where you have multiple 'test' jobs hooked up as downstream jobs of a 'build' job. You'll then configure the build job so that the build gets promoted when all the test jobs passed successfully. This allows you to keep the build job run fast (so that developers get faster feedback when a build fails), and you can still distinguish builds that are good from builds that compiled but had runtime problems.

**阅读同主题内容**

- [高效Jenkins用户的第1个习惯](http://euccas.github.io/blog/20151210/jenkins-user-habits-1.html)
- [高效Jenkins用户的第2个习惯](http://euccas.github.io/blog/20151215/jenkins-user-habits-2.html)
- [高效Jenkins用户的第3个习惯](http://euccas.github.io/blog/20160523/jenkins-user-habits-3.html)
- [高效Jenkins用户的第4个习惯](http://euccas.github.io/blog/20161010/jenkins-user-habits-4.html)
- [高效Jenkins用户的第5个习惯](http://euccas.github.io/blog/20161216/jenkins-user-habits-5.html)