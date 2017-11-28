---
layout: post
title: "C++ Functors"
date: 2017-01-15 20:20:07 -0800
comments: true
categories: C++
keywords: C++ Functor
description: Introduce C++ Functor, C++ Functor usage
---

A **functor** is a powerful C++ entity that everyone who wants to master C++ needs to know. A functor, which is short for "**function object**", is a C++ class that acts like a function. Functors can be called using the familiar function call syntax, and can yield values and accept parameters just like regular functions. 

To create a functor, we create a class (or a struct) that overloads the function ```operator()```. Note here the function is called ```operator()```, and it's not the ```operator``` function, i.e. ```()```. We then create an instance of this class (or struct) to use the created functor. 
 
# Create and use functors

Let's look at two examples of creating and using a functor. In the first example, a functor is created with a ```class```, and in the second example we use a ```struct``` to create the functor.  

<!--more--> 

## Example: Create a functor with a Class

```c

class MyFunctor {
public:
    void operator() (const string& str) const {
        cout << str << endl;
    }
}

// Using functor:

MyFunctor functor; // create an instance of the functor class
functor("This is a functor!"); // and "call" it

// equivalence:
cout << functor.operator()(23) << endl;

// You'll see "This is a functor" printed out.

```

## Example: Create a functor with a Struct

```c

struct add_x {
  add_x(int x) : x(x) {}
  int operator()(int y) { return x + y; }
private:
  int x;
};

// Using functor:

add_x add42(42); // create an instance of the functor class
int i = add42(8); // and "call" it
assert(i == 50); // and it added 42 to its argument

std::vector<int> in;
std::vector<int> out;
// Pass a functor to std::transform, which calls the functor on every element 
// in the input sequence, and stores the result to the output sequence
std::transform(in.begin(), in.end(), out.begin(), add_x(1)); 
assert(out[i] == in[i] + 1); // for all i

```

# Functors access class data members

The key difference between a function and a functor is that a functor's function call operator is a *member function* whereas a raw C++ function is a *free* function. This means that a functor can access the following information when being called:

* Its local variables
* Its parameters
* Global variables
* **Class data members**

If a functor's ```operator()``` member function requires access to data beyond what can be communicated by its parameters, we can store that information as a data member inside the functor class. Since ```operator()``` is a member of the functor class, it can then access that data freely. The following example shows how a functor's ```operator()``` function access the class's private member ```toAppend```. 

```c

class StringAppender {
public:
    // Constructor takes and stores a string.
    explicit StringAppender(const string &str) : toAppend(str) {}
    
    // Operator() prints out a string, plus the stored suffix.
    void operator() (const string &str) const {
        cout << str << ' ' << toAppend << endl;
    }

private:
    const string toAppend;
};

// Usage:
StringAppender myFunctor("is awesome");
myFunctor("C++");

// You'll see "C++ is awesome" is printed out.

```

# Functors are useful in STL algorithms

C++ STL algorithms use functors to increase the flexibility and efficiency. The most common uses for function objects are for generating data, for testing data, and for applying operations to data. here is an example of how STL ```for_each``` uses functors.

```c

struct sum
{
    sum(int* t):total(t){};
    int* total;
    void operator()(int element)
    {
       *total += element;
    }
};

int main()
{
    int total = 0;
    sum s(&total);
    int arr[] = {0, 1, 2, 3, 4, 5};
    std::for_each(arr, arr+6, s);
    cout << total << endl; // prints total = 15;
}

```

*The reader of [Stanford course CS106l](http://web.stanford.edu/class/cs106l/course-reader/Ch13_Functors.pdf) explains functors in detail.*