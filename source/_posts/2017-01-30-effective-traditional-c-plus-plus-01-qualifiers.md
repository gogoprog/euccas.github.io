---
layout: post
title: "Effective Traditional C++ (1): Qualifiers"
date: 2017-01-30 21:41:11 -0800
comments: true
categories: C++
keywords: C++
description: Tips and tactics for C++
---

Recently I'm doing a review on C++ programming language. During the process, I found a few topics which are worth paying more attention to. I'll write several posts about the related C++ tips and tactics. These topics are not specially for C++ 11 or 14, I therefore name this series of posts as "Effective Traditional C++". 

The first topic I'll write about here is: **Qualifiers**

C++ uses Qualifiers to adjust qualities of a variable or an object. In C++, there are two types of qualifiers: CV qualifiers and storage qualifiers.

# CV Qualifiers

CV qualifiers stands for Const and Volatile Qualifier. There are three types of CV qualifiers:

* const
* volatile
* mutable

## const qualifier

<code>const</code> marks a variable or function as read-only or immutable. It's value (or the return value of a function) cannot be changed once it's been defined.

```

const int weekdays = 7;

const int * myptr1; // declares myptr1 is a pointer to a constant integer
int const * myptr2; // same as above, declares myptr2 is a pointer to a constant integer
// myptr1 and myptr2 can be changed to point to other const integers

int * const  myptr3; // declares myptr3 is constant pointer to a variable integer
int const * const myptr4; // declares myptr4 is constant pointer to a constant integer
// myptr3 and myptr4 cannot be changed once initialized

const char *Function1()
{ return "Some text";}

```


## volatile qualifier

<code>volatile</code> marks a variable that may be **changed by another process**. This is generally used for threaded code, or externally linked code. Often <code>volatile</code> is used to tell the compiler avoid aggressive optimization involving the qualified object because the value of the object might be changed by means that the compiler is not aware of.

```

volatile int maxcnt = 10;
int cnt = 0;
while (cnt < maxcnt)
{
    // do something ... 
}

```

## mutable qualifier

<code>mutable</code> is used on data member to make it writable from a <code>const</code> qualified member function.

```

class A {
   mutable int x;
   int y;

   public:
     void f1() {
       // "this" has type `A*`
       x = 1; // okay
       y = 1; // okay
     }
     void f2() const {
       // "this" has type `A const*`
       x = 1; // okay, because x is mutable qualified
       y = 1; // illegal, because f2 is const
     }
};

```

# Storage Qualifiers

Storage qualifiers determine the lifetime of the defined variables or functions. By default, a variable defined within a block has automatic lifetime, which is the duration of the block. There are three types of storage qualifiers:

* static
* register
* extern

## static qualifier

<code>static</code> marks the variable is alive for the duration of the program. Static variables are commonly used for keeping **state** between instances of a given function or method. Static variables are stored globally, even if they are stored in a class. 

## register qualifier

<code>register</code> marks the variables as register variables, which are stored in processor registers. Register variables are faster and easier to access and operate on. Note using <code>register</code> only suggest the compiler that particular automatic variables should be allocated to CPU registers, if possible. The compiler may or may not actually store the variable in a register. Register variables should only be used if you have a detailed knowledge of the architecture and compiler for the computer you are using. 

## extern qualifier

<code>extern</code> defines the variables or functions in a separate translation unit and are linked with the code by the linker step of the compiler. In other words, you can **define** variables or functions in some source files or classes, and use them in other source files/classes by using <code>extern</code> qualifier to **declare** them in other source files or classes. 

