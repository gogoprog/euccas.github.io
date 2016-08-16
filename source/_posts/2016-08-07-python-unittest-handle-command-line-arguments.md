---
layout: post
title: "Python Unittest: Handle the command line arguments"
date: 2016-08-07 11:57:32 -0700
comments: true
categories: python unittesting
---

In the previous post about [Python Unittest](http://euccas.github.io/blog/20160711/start-unit-testing-in-python.html), I wrote about the basic steps needed for setting up unit testing for your Python program with the <code>unittest</code> module. In this post, I'll discuss about handling the command line parameters that your program need while you're using Python <code>unittest</code>.

Unit testing is meant for testing basic functionality of the application. The target of [Unit testing](https://en.wikipedia.org/wiki/Unit_testing) is expected to be each function of your program. When your program has command line arguments, ideally the unit tests should not accept arguments from the command line because unit tests are supposed to be very specific and not testing on the [Integration level](https://en.wikipedia.org/wiki/Integration_testing) (i.e. across multiple functions in your program).

So the way I use to handle the command line arguments can be summarized as: 

- Refactor your program to have the arguments parsing as a function
- Refactor your program to handle the arguments parsing differently when doing unit testing
- In the unit tests, set the arguments and pass them directly to the functions under test

The following is a demo Python project I built to demonstrate handling command line arguments when using <code>unittest</code>.

## myapp.py

    #!/usr/bin/env python

    import sys, os.path, re
    import argparse

    class myApp():
    
        EXIT_PASS, EXIT_FAIL = 0, 1
    
        def __init__(self, mode = 'normal', test_param = None):
            # Validate and process argument options
            self.parse_args(mode, test_param)
            # Initialize database connection
            self.app_name = self.get_app_name(self.name)

        def parse_args(self, mode, test_param):
            if mode == 'unittest':
                if test_param is None:
                    print("Missing test param")
                    self.app_exit('fail')

                self.name = test_param['app_name']
                self.verbose = test_param['verbose']
            else:
                parser = argparse.ArgumentParser(description='myApp: A demo project')
                parser.add_argument('-n', '--name', help='Name of myApp', required=True)
                parser.add_argument('--verbose', action='store_true', help='Verbose mode with more information printed')

                args = parser.parse_args()

                self.name = args.name
                self.verbose = args.verbose

        def app_exit(self, status):
            if status.lower() == 'pass':
                print("** App Exit Status: PASS \n")
                exit(self.EXIT_PASS)
            elif status.lower() == 'skip':
                print("** App Exit Status: SKIP \n")
                exit(self.EXIT_PASS)
            else:
                print("** App Exit Status: FAIL \n")
                exit(self.EXIT_FAIL)

        def get_app_name(self):
            app_name = self.name

            return app_name

    if __name__ == '__main__':
        app = myApp()

## test_myapp.py

    #!/usr/bin/env python

    import sys, os.path, re
    import argparse
    import unittest

    bin_path = os.path.dirname(os.path.realpath(__file__))
    lib_path = os.path.abspath(bin_path)
    sys.path.insert(0, lib_path)

    import myApp

    class myAppTestCase(unittest.TestCase):

        def setUp(self):
            mode = 'unittest'
            test_param = {
                'name': 'Test App',
                'verbose': True
            }
            self.app = myapp.myApp(mode, test_param)

        def test_app_name(self):
            self.assertEqual(self.app.get_app_name, 'Test App', 'Wrong App Name')

        def tearDown(self):
            print('Bye Test')

    if __name__ == '__main__':
        unittest.main()

