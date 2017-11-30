---
layout: post
title: "Python: Why Decorators are useful"
date: 2017-11-29 22:41:51 -0800
comments: true
categories: Python
keywords: Python Decorators
description: An introduction to Python Decorators, why they are useful, and when you will need use decorators
---

In Python, by definition **decorators** are *functions* that *accept a function* as an argument, and *return a new function* as their return value. The reason why decorators exist in Python, but not in other similar language such as Ruby, is that *functions* are *objects* in Python. Functions can be assigned to variables and passed around the same as other object in Python. For example, a list can have functions as its elements, and functions can take other functions as arguments. Functions can be defined inside another function, and this forms closures.

# When to use decorators?

It's easy to understand what decorators are, while the real question you may have is: Why decorators are useful? When shall I use decorators in my Python program?

In some way, I see decorator functions are useful whenever you need process or extend the inputs or outputs of a given function (or more often, multiple functions) in some way you want. Here I list three usages of decorators that I can think of:

## 1. Extend the functionality of your functions

Usually the extended functionalities are for some kind of enhancement, format changing, or temporary usage. In other words, you are adding some functionalities without touching the core logic of the original functions. A few common use cases:

- Convert the output of your functions to another format, like JSON, YAML, etc.
- Add logging to your functions, or formatting the logging output
- Measure timing of your functions
- Count the time of function calls

## 2. Add caching process to your functions, to make them faster

When you have some functions which are possibly called for many times with the same input, you can write a decorator function that stores a cache of inputs and outputs of a given function. In this way, the function doesn't need to re-compute everything each time, and make it faster to run it multiple times. This is related to the [**Memoization technique**](https://en.wikipedia.org/wiki/Memoization).

## 3. Handle exceptions

You can use decorator functions to process exceptions. One example is supressing particular types of system exceptions raised by the target function. Another thing you can do is catching all exceptions raised by a function, prompt the user to ask what the program should act.


# Two examples

Now let me use two examples to describe the **syntax** of decorators.

## Measure timing

This example comes from a good answer on [Stack Overflow user RSabet](https://stackoverflow.com/a/490228/3109254).

A decorator function ```time_dec``` tells you how long it takes to finish a function. 
Python has a shortened syntax for using decorators which allows us to wrap a function in a decorator after we define it. This shortened syntax is syntactic sugar ```@decorator_function```.  

```python
def time_dec(func):
    def wrapper(*arg):
        t = time.clock()
        res = func(*arg)
        print(func.func_name, time.clock()-t)
        return res
    
    return wrapper


@time_dec
def myFunction(n):
    ... 

```


Note the syntactic sugar ```@time_dec``` was used. It causes Python to rebind the function name ```myFunction``` as:
 
```python
myFunction = time_dec(myFunction)

```
 
## Memoization

This example shows how we can add caching to the calculation of prime numbers.

A decorator function ```memoize``` is used to store inputs and calculate outputs of the original function ```is_prime```.
The second time when you call function ```is_prime``` with the same input number, it runs much faster than the first time.

```python
def memoize(func):
    cache = {}
    def new_func(*args):
        if args not in cache:
            cache[args] = func(*args)
        return cache[args]
    return new_func

@memoize
def is_prime(number):
    for n in range(2, number):
        if number % n == 0:
            return False
    return True

```


# Built-in decorators

Python also has several built-in decorators, and you might see them before you know the term decorator. The built-in decorators are mainly used to annotate methods of a class: ```@property```, ```@classmethod```, ```@staticmethod```. 

**@property**: transforms a method function into a descriptor. When applied to a method, it creates extra properties objects: ```getter```, ```setter```, and ```deleter```. By using ```@property```, we can access a method as if it was an attribute.

**@classmethod**: transforms a method function into a class-level function.

**@staticmethod**: transforms a method function into a class-level function, and neither the object instance nor the class is implicitly passed as the first argument.

As decorators are just ordinary functions and the decorator syntax is just a syntactic sugar, you can easily turn any Python [built-in function](https://docs.python.org/3/library/functions.html) to a decorator if it makes sense to use it that way. 


# One more thing

One more thing, you may want to take a look at [this PythonDecoratorLibaray page](https://wiki.python.org/moin/PythonDecoratorLibrary). It collects a number of decorator examples and code pieces.
