---
layout: post
title: "Rake: Automake your tasks in Ruby"
date: 2016-06-14 17:59:06 -0700
comments: true
categories: Ruby
---

Rake is the build language for Ruby programs, originally developed by [Jim Weirich](http://onestepback.org/). It's a standard library in Ruby 2.1. You can define tasks with Rake: named code blocks that carry out specific actions, such as running unit tests, deploy your code to github, etc. In this post, I'll write about the basics of Rake and how to use it to automate the tasks of your Ruby projects.


# Rakefile

In order to use Rake to define tasks, first you need a Rakefile. A Rakefile is a Ruby source file that has access to some special methods: **task**, **file**, **directory**, and a few others. A task defined in the Rakefile can be run by the command-line ```rake``` program, or be called as a dependency by other tasks. The name of Rakefile can be ```Rakefile``` or ```rakefile```.

<!--more--> 

# Write Descriptions for Rake Tasks

Writing a description to the defined tasks in Rakefile help you get more details about the task and know better what it does.

Example:

```ruby
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

```ruby
namespace :cleanup do
    desc 'Clean up database'
    task  :dbs => :environment do
        Db.cleanup
    end

    desc 'Clean up logs'
    task :logs => :environment do
        Log.cleanup
    end

    task :all => [:dbs, :logs]
end

desc 'Cleanup everything'
task :cleanup => "cleanup:all"

```

# Default Task

The default task is the one gets executed when you run rake without any arguments. You can set the default task in Rakefile by using the ```:default``` keyword.

```ruby
task :default => 'cleanup'
```

```ruby
task :default => 'logs: cleanup'
```

# Multiple Tasks Running in Parallel

Rake's ```multitask``` function supports running multiple tasks in parallel. The method is defining a task using the ```multitask``` function, and each of this task's prerequisites will be run in a separate thread.

An example of multiple parallel tasks:

```ruby
task 'copy_docs' do
    # Simulate a large disk copy
    sleep 5
end

task 'compile_extensions' do
    # Simulate a C compiler compiling a bunch of files
    sleep 10
end

task 'build_serial' => ['copy_docs', 'compile_extensions]
multitask 'build_parallel' => ['copy_docs', 'compile_extensions']

```

In this example, the ```build_serial``` task runs in about 15 seconds, but the ```build_parallel``` task runs in about 10 seconds.

# Invoke tasks

Rake tasks can be invoked from other tasks using the ```Rake::Task['<your take>'].invoke``` method.

```ruby
task :cleanup do
    Rake::Task['logs: cleanup'].invoke
    puts "logs are cleaned!"
    Rake::Task['dbs: cleanup'].invoke
    puts "dbs are cleaned!"
end

```

# View all the Rake tasks

To get an overview of all the defined Rake tasks, use ```rake -T```

# Include external rakefiles

When your project need include the Rake tasks defined in external directories, you'll need include the external rakefiles into your project. The way to do it is using the ```import```. Note the ```require``` won't work here, as it looks for the ```.rb``` files instead of the ```.rake``` files.

Include one rakefile:

```ruby
import File.dirname(__FILE__)+"/../../task/common/rakefile"
```

Include multiple rakefiles in nested directories:

```ruby
Dir.glob("#{File.dirname(__FILE__)}/*").each do |d|
  next if !File.directory? d
  import d + "/rakefile" if File.file?(d + "/rakefile")
end

```

# Exit from Rake tasks

In a Ruby function, you can use ```return``` in the function when you want to exit (early). But in Rake tasks, the ```return``` is an invalid method to use, because each Rake task is actually a ```Proc```. To exit early from a Rake task, you can use one of the following methods:

- next

***next*** will discard the following codes in the current rake task, and process the following part of the other tasks if there are any.

- fail/raise

```ruby
task :something do
  [1,2,3].each do |i|
    ...
    fail "some error" if ...
  end
end

```

- exit

- abort

When ***abort*** is used in a rescue block, it terminates the task as well as prints the whole error (even without using --trace).


# Reference

- [Ruby Cookbook 2nd Edition (L. Carlson)](https://www.amazon.com/Ruby-Cookbook-Lucas-Carlson/dp/1449373712)
- [Using the Rake Build Language (Martin Fowler)](http://martinfowler.com/articles/rake.html)
