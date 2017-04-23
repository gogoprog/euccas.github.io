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

<!--more--> 

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

There is no particular required folder structure that you need to keep your test files. The way I usually do is separating the tests from the project source files. So, I create a <code>test</code> folder in the same level as ```dev```. All my tests will be put into this folder. Now the project's structure looks like:

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

## 3. Include your project modules in the test

Surely you'll need include the source files of the modules that you want to test in your test file. If your tests are in the same folder of your module sources, you can simply use <code>import SomeModule</code> to pull the modules in. When your tests stay out of the module sources, you'll need do a little configurations in your test file.

I found the way to import your own modules to your tests can be different depending your development environment. For example, if you run your Python projects within some IDE, like **PyCharm** from JetBrains. The following way always work:

```

# This is test/test_demoDev.py

from dev import demoDev

```

However if you run through command line ```python test/test_demoDev.py```, you might see errors complaining no module called <code>dev</code> and thus the import fails.

What you can do to resolve this problem, is adding the path of your Python modules to the <code>sys.path</code>.

```

# This is test/test_demoDev.py

import sys, os.path

bin_path = os.path.dirname(os.path.realpath(__file__))
lib_path = os.path.abspath(os.path.join(bin_path, '..', 'dev'))
sys.path.insert(0, lib_path)
# or sys.path.append(lib_path)

import demoDev


```

## 4. Create a test case

A test case can be created with unittest *TestCase* class. The <code>setUp()</code> and <code>tearDown()</code> methods can be overridden to provide initialization and cleanup for the fixture. Each instance of the TestCase will only be used to run a single test method. Multiple test methods share the same text fixture, but the test fixture are created for each test method when they are executed.

```

# This is test/test_demoDev.py

import sys
import unittest

bin_path = os.path.dirname(os.path.realpath(__file__))
lib_path = os.path.abspath(os.path.join(bin_path, '..', 'dev'))
sys.path.insert(0, lib_path)

from dev import demoDev

class demoDevTestCase(unittest.TestCase):

    def setUp(self):
        self.checker = eABTCheckerDev.eABTChecker()

    def test_checker_app(self):
        self.assertEqual(self.demo.app, 'Demo App', 'Wrong app')

    def tearDown(self):
        print('Bye Test')

if __name__ == '__main__':
    unittest.main()

```

The <code>TestCase</code> class provides several assert methods to check for and report failures, such as <code>assertEqual</code>, <code>assertNotEqual</code>, <code>assertTrue</code>. [Here is the complete assert list that Python 3 provides.](https://docs.python.org/3.4/library/unittest.html#assert-methods)

## 5. Create more tests and a test suites

<code>TestSuite</code> class represents an aggregation of individual test cases and test suites. The <code>addTest</code> and <code>addTests</code> methods are available to add tests to your TestSuite instances.

```

# This is test_demoDev.py

def suite():
    suite = unittest.TestSuite();
    suite.addTest(demoDevTestCase('test_checker_app'))
    suite.addTest(demoDevTestCase('test_check_env'))
    
    return suite

```

# 6. Run your unit tests!

The easiest way to run your unit tests is executing the <code>unittest.main()</code> method in the test file.

```

# This is test_demoDev.py

if __name__ == '__main__':
    unittest.main()

```

Then by running command <code>python test_demoDev.py</code>, the tests defined in <code>test_demoDev.py</code> will start running.

Unit tests can run from command line, because ```unittest``` module can be used from the command line to run tests from modules, classes or individual test methods.

```

python -m unittest test_demoDev.test_checker_app

```

You'll see the testing result like:

```

----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
Bye Test

Process finished with exit code 0

```

Behind the tests running, there is the <code>run</code> method provided by <code>TestCase</code> and <code>TestCaseSuite</code> classes. This <code>run</code> method implements the function of running the test, collecting the result into the <code>TestResult</code> object passed as result.

Here you go! Enjoy unit testing in Python!
