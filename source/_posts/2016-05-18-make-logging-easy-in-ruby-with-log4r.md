---
layout: post
title: "Make logging easy in Ruby with log4r"
date: 2016-05-18 16:18:07 -0700
comments: true
categories: Ruby
---

Log4r is a Ruby gem that features a heirachical logging system of any number of levels, custom level names, multiple output destinations per log event, custom formatting, and more. The Log4r gem is open sourced on [GitHub](https://github.com/colbygk/log4r), and with comphrehensive documentations available on [Rubyforge](https://github.com/colbygk/log4r).

I have been using log4r at work in most of the applications and systems written in Ruby. It's easy to use, and provide the features that an application would need:
- Support multiple message levels such as Fatal, Error, Warn and Msg.  
- Customizable log file format
- Multiple output destinations, like print out on the screen, and store in a log file

Here in this post, I'll show you how to use log4r in your Ruby project.

## Step 1. Install Gem log4r
```
gem install log4r
```

## Step 2: Include log4r in your project

One thing to note is the log4r supports configurations through YAML file, and you can define the configuration file when including the log4r.

```
require 'log4r'
require 'log4r/yamlconfigurator'
require 'log4r/outputter/datefileoutputter'
require 'log4r/outputter/emailoutputter'
include Log4r
ycfg = YamlConfigurator    # handy shorthand
ycfg.load_yaml_file(File.dirname(__FILE__)+'/l4r.yml')
```

## Step 3: Configure log4r with a config file

You can define the logging levels, logger names, output destinations, etc. The following code shows an example of the configurations that I use.

File name: log4r.yml

```

description: config file for log4r

---
# *** YAML2LOG4R ***
log4r_config:
  # define all pre config ...
  pre_config:
    global:
      level: DEBUG
    root  :
      level: DEBUG

  # define all loggers ...
  loggers:
    - name      : myproject 
      level     : DEBUG
      additive  : 'false'
      trace     : 'false'
      outputters:
        - stderr
        - logfile
        - email


  # define all outputters (incl. formatters)
  outputters:
    - type     : StderrOutputter
      name     : stderr 
      level    : INFO
      formatter:
        date_pattern: #'%y%m%d %H:%M:%S'
        pattern     : '[%c] %l: %m'
        type        : PatternFormatter

    - type        : DateFileOutputter
      name        : logfile
      level       : DEBUG
      date_pattern: #'%Y%m%d'
      trunc       : 'false'
      dirname     : "."
      formatter   :
        date_pattern: '%H:%M:%S'
        pattern     : '[%c] %d %l: %m'
        type        : PatternFormatter
  
    - type        : EmailOutputter
      name        : email
      level       : FATAL 
      server      : <server domain>
      subject     : 'Message myproject:'
      from        : <email address>
      to          : <email address>
      formatter   :
        date_pattern: #'%y%m%d %H:%M:%S'
        pattern     : '%d %l: %m'
        type        : PatternFormatter
---
```

## Step 4: Initialize a logger

You need initialize a logger in your project first.

```
logger = Log4r::Logger['myproject']
```

## Step 5: Use your logger

```
logger.info 'My Project Starts!'
logger.warn 'Here is a warning'
logger.error 'Here is an error'
logger.fatal 'Fatal error happens. Program will exit'
```

