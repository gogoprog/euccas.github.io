---
layout: post
title: "Python Generators"
date: 2016-12-23 08:48:45 -0800
comments: true
categories: Python
---

Generators is a powerful weapon of Python. Generators help you write concise code, give you lazy evaluation, and improve the efficience for calculating large sets of results. Personally I think it's a good habit to use generators in Python whenever you can, if you really want your code to be Pythonic.

# How to create a generator

There are mainly two ways to create a generator: using the ```yield``` keyword in the function, or using the ```()``` as a generator expression. 

* The ```yield``` keyword makes the function yields control back to the calling function on every iteration
* The ```()``` expression returns a generator object

<!--more--> 

# How to refactor a function to use a generator

Functions that construct a list or another iterable and returns it can be turned into a generator by:

1. Converting the list append into a ```yield```
2. Removing the empty list creation
3. Removing the return

# A generator example
Let's see an example: implement a function that takes a list and return a list of the current running mean. For example, given the input list ```[8, 4, 3, 1, 3, 5]```, the expected return result is ```[8.0, 6.0, 5.0, 4.0, 3.8, 4.0]```. 

First we'll implement it without using generators.

```python
def running_mean(numbers):
	average = []
	sum = 0
	for i, num in enumerate(numbers):
		sum += num
		average.append(sum/(i*1.0))
	return average

numbers = [8, 4, 3, 1, 3, 5]
print(running_mean(numbers))

```

Now we can refactor the above implementation to use a generator:

```python
def running_mean(numbers):
	sum = 0
	for i, num = enumerate(numbers):
		sum += num
		yield sum/((i+1)*1.0)

numbers = [8,4,3,1,3,5]
print(list(running_mean(numbers)))

```

What we did in the refactoring was: replacing the list appending with a yield (```average.append()```), removing the empty list creation (```average = []```), and replacing the return statement with a yield statement.

One important property of Python generator object is it is a single-use object. In other words, a generator keeps yielding answers forever. The looping in a generator only ends when the calling function decides to end it. Meanwhile a generator can only be called once.

A few other generator examples can be found on my [GitHub repo *IntermediatePython*](https://github.com/euccas/IntermediatePython/tree/master/iteration/generator)


