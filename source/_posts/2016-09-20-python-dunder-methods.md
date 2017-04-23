---
layout: post
title: "Dunder Methods in Python"
date: 2016-09-20 20:28:51 -0800
comments: true
categories: python
---

In Python, we sometimes see method names with ```__``` around, such as the ```__init__``` method that every Class has. These methods are "dunder" methods ("dunder" stands for "double under" or "double underscore"). Dunder methods in Python are used for operator overloading and customizing behavior of other functions.

Sometimes dunder methods are also called "magic methods" because they are usually called by Python under the hood. But they are not really magical, you can define dunder methods to customize the behavior of your own classes.

# Examples of Dunder Methods

<!--more--> 

In the following example, we can see three dunder methods:

- ```__init__``` method: is called to initialize the class
- ```__str__``` method: is called when converting the object to a human-readable string
- ```__repr__``` method: is called when converting the object to a developer-readable string

```
    class Flower:
	    def __init__(self, color='red'):
		    self.color = color

		def __str__(self):
			return "Flower in color {color}".format(color=self.color)

		def __repr__(self):
		return "Flower(color={})".format(self.color)
```

In Python, many dunder methods are implemented and used for operations such as arithmetic operators, comparison operators, truthiness, etc. The following are a few examples:

**Arithmetic Operators**

- ```+``` : ```__add__```
- ```-``` : ```__sub__```
- ```*``` : ```__mul__```
- ```/``` : ```__div__```

**Comparison Operators**

- ```x < y``` : ```x.__lt__(y)```
- ```x <= y``` : ```x.__le__(y)``` 
- ```x > y``` : ```x.__gt__(y)```
- ```x >= y``` : ```x.__ge__(y)```
- ```x == y``` : ```x.__eq__(y)```
- ```x != y``` : ```x.__ge__(y)```

If you know about Bash shell, you may notice the name of these dunder methods are very similar to the operators in Bash.

**Truthiness**

- ```bool(x)``` : ```x.__bool__()```

# Use Dunder Methods to Customize Class Behaviors

Dunder methods provide a way for our class to customize operators and other built-in Python behavior for our objects. In the following two examples, I'll use dunder methods to overload arithmetic operators, and implement a dictionary that can be used with both attribute and item syntax.

## Example 1: Overload Arithmetic Operators

Make an ```is_callable``` function to check if an object type is callable.

Example:

```
    >>> is_callable(sorted)
    True
    >>> is_callable(str)
    True
    >>> is_callable(4)
    False
```

Source Code:

```
    def is_callable(obj):
    
    try:
    	obj.__call__
    	# hasattr(str, '__call__')
    	# getattr(str, '__call__')
    except AttributeError:
    	return False
    else:
    	return True
```

## Example 2: Class EasyDict

Make an ```EasyDict``` class that can be used with both attribute and item syntax.

Example:

```
	>>> a = EasyDict()
	>>> a['shoe'] = "blue"
	>>> a.shoe
	"blue"
	>>> a['shoe']
	"blue"
	>>> a.car = "green"
	>>> a['car']
	"green"
```

Source Code:

```
	class EasyDict:
    	def __init__(self):
        	pass

   		def __getitem__(self, item):
        	return self.__dict__[item]

    	def __setitem__(self, key, value):
        	self.__dict__[key] = value

```



