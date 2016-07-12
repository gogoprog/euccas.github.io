---
layout: post
title: "Start Unit Testing in Python"
date: 2016-07-11 22:58:39 -0700
comments: true
categories: Python UnitTesting
---

When is the best time to start unit testing in your Python project? My answer is before you writing the first line of code of this project. Unit testing is the fundamental of Test-driven development, which specifically improves the quality and design of your project. 

In this post, I'm writing about how could you do unit testing in Python with the ```unittest``` module.

Python 2 (starting on version 2.1) and Python 3 now both have ```unittest``` in the standard library. The ```unittest``` module provides the unit testing framework, and it's based on ```JUnit```, which is a unit testing framework for Java. 

# What unittest can do

A few main features that ```unittest``` can do are:
- Automatically run the tests (by ```test runner```)
- Create test cases (by ```test case```)
- Sharing of setup and shutdown code for tests (by ```test fixture```)
- Aggrate tests into collections (by ```test suite```)
- Independence of the tests from the reporting framework

# How does unittest work

Suppose I'm working on a project called ```demo```, and it has a file structure as:

```
demo
-- dev
   -- __init__.py
   -- demoDev.py
```

Note the ```___init___.py``` file can be empty. The purpose of having this file is for other files outside this directory can easily import the module ```demoDev.py```.

To create unit tests for this project, I'll need continue the following steps.

## 1. Create the test file

There is no particular required folder structure that you need to keep your test files. The way I usually do is separating the tests from the project source files. So, I create a ```test``` folder in the same level as ```dev```. All my tests will be put into this folder. Now the project's structure looks like:

```
demo
-- dev
   -- __init__.py
   -- demoDev.py
-- test
   -- test_demoDev.py
```

## 2. Use unittest module in your project

The test file need import the ```unittest``` module.

```
# This is test/test_demoDev.py

import unittest
```

