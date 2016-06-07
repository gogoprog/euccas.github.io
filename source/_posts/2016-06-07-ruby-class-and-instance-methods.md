---
layout: post
title: "Ruby Class and Instance Methods"
date: 2016-06-07 11:37:51 -0700
comments: true
categories: Ruby 
---

If you ever get confused about Class Methods, Instance Methods, Class Variables and Instance Variables in Ruby, read this post and you'll understand it better :)

# Class Methods
- Class methods belong to a class in Ruby, and it can be used without instance any class object. 
- The definition of class methods has a "self" prefix.

```
def self.show_name
end
```

# Instance Methods
- Instance methods belong to any instance of a class in Ruby. To use instance methods, you always need to have an existing instance first. Usually this means you have called ```new()``` method.
- Instance methods do not have "self" prefix in their definition.

```
def show_name
end
```

# Class Variables
- Class variables belong to a class in Ruby. In other words, each class in Ruby automatically has an object even without any instances. The class variables are constants of the class object.
- Class variables are totally separated with instance variables (obvious though). The value of a class variable doesn't change when the instance variables having the same name change.
- The name of a class variable has the "@@" prefix.

```
class myClass
    @@foo = 0
end  
```

# Instance Variables
- Instance variables belong to an instance of a class in Ruby.
- Different instances have their own set of instance variables.
- The name of an instance variable has the "@" prefix.

```
class myClass
    def initialize()
        @foo = 0
    end
```

# A quick demo

So now I have a quick demo to show more about the Class/Instance methods and variables.

In this demo, a Fruit class is created. The Fruit class has a ***class variable*** ```@@color```, and the Fruit class instances have a ***instance variables*** ```@color```.

Fruit class has a class method ```self.show_color```, and an instance method with the same name ```show_color```.

Now check out how these stuff works.

```
# fruit.rb

class Fruit
    @@color = 'yellow' # class variable

    def initialize()
        @name = 'apple'
        @color = 'red' # instance variable
    end

    def self.show_color()
        puts "(class method) color: #{@@color}"
    end

    def change()
        change_color()
        puts "try calling instance method"
        show_color()
        puts "try calling class method"
        self.show_color()
        puts "change done"
    end

    def change_color()
        @color = 'green'
    end

    def show_color()
        puts "(instance method) color: #{@color}"
    end
end
```

The test file:

```
# test.rb

$LOAD_PATH.unshift(File.expand_path(File.dirname(__FILE__)))
require 'fruit.rb'

myfruit = Fruit.new
myfruit.show_color
myfruit.change

Fruit.show_color
```

Executing the ```test.rb``` file will generate the following result:

```
(instance method) color: red
try calling instance method
(instance method) color: green
try calling class method
(instance method) color: green
change done
(class method) color: yellow
```

## Summary of the demo

- ```<Class>.new``` instances an object by calling the ```initialize``` method. Instance variables are initialized

- Instance methods only calls the instance methods within itself, even use the ```self``` prefix.

```
show_color()
self.show_color()
```

Both call the instance method, and shows the ```color: green```

- The change on instance variables doesn't affect the class variables

- Class methods can be called without instances
```
Fruit.show_color
```
- Instance methods can't be called without instances. The following statement will exceptions (NoMethodError).

```
myfruit = Fruit.new
myfruit.add

# undefined method `add ... (NoMethodError)
```

