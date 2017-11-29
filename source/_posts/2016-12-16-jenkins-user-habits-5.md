---
layout: post
title: "高效Jenkins用户的第5个习惯"
date: 2016-12-16 15:49:51 -0800
comments: true
categories: Jenkins Continuous-Integration 中文
---

本文内容部分来源于**Andrew Bayer**发布在SlideShare上的 [*7 habits of highly productive Jenkins Users (2014 Edition)*](http://www.slideshare.net/andrewbayer/seven-habits-of-highly-effective-jenkins-users-2014-edition).

# 习惯 5: 集成第三方工具和服务

Jenkin可以和许多第三方工具和服务集成，实现强大又实用的功能。常见的集成方式包括使用REST API和一些Jenkins功能插件。可以实现的功能比如：由GitHub pull requests触发builds，当builds成功或失败时根据结果更新JIRA等等。

<!--more--> 

## Gerrit和Github的pull requests

一些非常实用的Jenkins builds工具和服务包括：

* Gerrit Trigger
* GitHub Pull Request Builder
* Jenkins Enterprise's version of GitHub pull request builder

Build工具和服务可以实现对每一次提交的改动进行build, 并且将结果报告提交代码审查工具。

在这些Build工具的基础之上，你可以实现自动化合并多个提交的改动，进行branch之间的同步等更多功能。

## [JIRA](https://www.atlassian.com/software/jira)

* 检查每一个commit的描述信息，如果其中包含有JIRA issue信息，就用commit信息（和测试结果）提交相应的JIRA issue更新
* 根据build的过程和步骤，更新所有相关项目的JIRA
* 生成JIRA release notes

## Artifactory

* 全局性地设定Jenkins jobs用于部署的证书信息 (credentials)
* 覆盖 (override) 每一个job的Maven distributionManagement 配置
* 定义Maven jobs和build步骤从何处获取artifacts
* 在Artifactory中保存build信息和关系

**阅读同主题内容**

- [高效Jenkins用户的第1个习惯](http://euccas.github.io/blog/20151210/jenkins-user-habits-1.html)
- [高效Jenkins用户的第2个习惯](http://euccas.github.io/blog/20151215/jenkins-user-habits-2.html)
- [高效Jenkins用户的第3个习惯](http://euccas.github.io/blog/20160523/jenkins-user-habits-3.html)
- [高效Jenkins用户的第4个习惯](http://euccas.github.io/blog/20161010/jenkins-user-habits-4.html)
- [高效Jenkins用户的第5个习惯](http://euccas.github.io/blog/20161216/jenkins-user-habits-5.html)
