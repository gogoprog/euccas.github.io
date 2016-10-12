---
layout: post
title: "Octopress Tips"
date: 2016-10-11 22:36:44 -0700
comments: true
categories: octopress, chinese
---

使用Octopress搭建这个blog已经有一段时间了，记录几个使用中需要注意的Tips.

# Tip 1: Clone Repo

如果需要重新复制一份已经存在的blog repo，在重新复制的blog repo上继续发布更新blog，那么需要注意：

首先复制的repo需要是source branch. 

如果repo的默认branch已经设定为source branch:

```
git clone <repo url>
```

如果repo的默认branch设定为master branch:

```
git clone <repo url>
git pull origin source
```

然后需要把master branch复制到```_deploy```目录。注意```_deploy```目录是在Octopress生成post的过程中必须存在的。

```
git clone <repo url> _deploy
cd _deploy
git pull origin master
```

# Tip 2: Push Changes to Source

使用```rake gen_deploy```将改动发布到```master branch```之后，还需要把source的改动也提交到```source branch```。

```
git push origin source
```

# Tip 3: Execute Rake Commands

如果因为```rake```版本问题造成```rake``` command不能够在repo中执行，就需要使用```bundle exec rake```执行。

```
bundle exec rake new_post
bundle exec rake generate
bundle exec rake preview
bundle exec rake deploy
```

# Tip 4: Errors in gen_deploy

```rake gen_deploy```的过程中，如果在```generate```步骤中出现错误（比如部分post的文本不符合markdown语法），一些情况下可能会造成generate目录中的文件被删除。而```gen_deploy```过程此时并不会结束，```deploy```会继续进行，这样最终的commit就会把原来已经发布的blog内容删除。防止出现这种问题的安全做法是分步执行```rake generate```和```rake deploy```。
