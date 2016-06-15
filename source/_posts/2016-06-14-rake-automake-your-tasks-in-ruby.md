---
layout: post
title: "Rake: Automake your tasks in Ruby"
date: 2016-06-14 17:59:06 -0700
comments: true
categories: Ruby
---

Rake is the build language for Ruby programs, originally developed by [Jim Weirich](http://onestepback.org/). It's a standard library in Ruby 2.1. You can define tasks with Rake: named code blocks that carry out specific actions, such as running unit tests, deploy your code to github, etc. In this post, I'll write about the basics of Rake and how to use it to automate the tasks of your Ruby projects.


# Rakefile

In order to use Rake to define tasks, first you need a Rakefile. A Rakefile is a Ruby source file that has access to some special methods: **task**, **file**, **directory**, and a few others. A task defined in the Rakefile can be run by the command-line ```rake``` program, or be called as a dependency by other tasks.

# Write Descriptions for Rake Tasks

Writing a description to the defined tasks in Rakefile help you get more details about the task and know better what it does.

Example:

```
desc 'Upload documentation to server'
task 'upload-docs' => ['rdoc'] do
    sh "scp -r #{html_dir}/* " + "#{user}:#{server_path}"
end

```

# Namespaces

Using namespaces is a good way to group similar tasks in Rakefile. You'll need specify the namespace when calling a task inside it. One example as you can see from Rails is this command

```
rake db:migrate
```

In this command, the ***db*** is the namespace, and the ***migrate*** is the task inside the namespace.



# Reference

- [Ruby Cookbook 2nd Edition (L. Carlson)](https://www.amazon.com/Ruby-Cookbook-Lucas-Carlson/dp/1449373712)
- [Using the Rake Build Language (Martin Fowler)](http://martinfowler.com/articles/rake.html)