---
layout: post
title: "Effective Traditional C++ (2): Pointer and Reference"
date: 2017-02-05 22:18:59 -0800
comments: true
categories: C++
keywords: C++
description: Tips and tactics for C++
---

Pointers and references are two fundamental data types in C++. They are useful, common and somewhat dangerous. Using them correctly, they could greatly improve the efficiency and performance of your program. On the other hand, using them incorrectly could lead to many problems such as memory leaks and buffer overflow.

# Pointers

A pointer holds the address of a variable and can be used to perform any operation that could be directly done on the variable, such as accessing and modifying it. Here are a few facts of pointers:

* When a pointer is defined, memory is allocated in the size of a pointer. 

* The pointer is strongly typed, meaning the compiler retains an association with a pointer that it points to a type of value. 

* Two pointers can equal to each other, such that changing one's value also changes the other's value.

```
int * p = new int;
*p = 1;
int * q = p;
*p = 2;
cout << *q; // Outputs 2. * is the pointer dereferene operator
```

* The size of a pointer varies depending on the architecture: 32 bits on a 32-bit machine and 64 bits on a 64-bit machine.

* Pointer subtraction is allowed. The result of pointer subtraction is the distance of two pointers.

```
int a = 1;
int b = 2;
int * pa = &a;
int * pb = &b;
int pdis = pa - pb;
```

* Adding a pointer and a distance gets another meaningful pointer.

```
int * p = new int[2];
p[0] = 0;
p[1] = 1;
p++;
cout << *p; // Outputs 1
```

* But adding two pointers won't give you a meaningful pointer. Don't do it.

# References

A reference is another name for a pre-existing object. It does not have memory of its own. In other words, a reference is only an alias. A few facts about references are:

* You cannot create a reference without specifying where in memory it refers to. A reference cannot be null.

```
int x = 7;
int & y = x; // Makes y a reference, initialized with the address of x
```

* You can create a free-standing reference as shown below:

```
const int & a = 12;
```

* A reference is immutable. You cannot reassign a reference to another piece of memory.

* When you use references in function calls and class method calls, you always want to make them const. This helps to eliminate the side effects of using references (because using reference sometimes is not obvious as using pointers, and people may not notice the unintended side effects could happen). The following example shows the possible side effects when using references:

```
int & f(int &x) {
    ++x;
    return x;
}

int main(int argc, char** argv)
{
    int i = 5;
    printf("the value is %d\n", i); // i is 5
    printf("the value is %d\n", f(i)); // f(i) is 6
    printf("the value is %d\n", i); // i is changed to 6 unindently
    return 0;
}

```

The good way is always using ```const``` when using references:

```
const int & f(const int & x) {
    static int y = x;
    ++y;
    return y;
}

int main(int argc, char** argv)
{
    int i = 5;
    printf("the value is %d\n", i); // i is 5
    printf("the value is %d\n", f(i)); // f(i) is 6
    printf("the value is %d\n", i); // i is 5
    return 0;
}
```

# Functions: Call by Reference

By default, functions in C++ pass variables by value, which means that a copy of the value is made and that copy is used inside the function. This is called **pass by value**. However, passing references or pointers does the same thing and faster as the copying is skipped. Actually this is why references are created for C++, to allow **call by reference** so that you can pass large objects without worrying about stack overflow.
 
 Before references, this can be done with pointers. Pass by pointers can do the same thing but it's a little bit more complicated than using references.
 
 Example of a "call by reference":
 
```
 void func(const string & fs)
 {
    print("string value is %s\n", fs.c_str());
 }
 
 int main(int argc, char ** argv)
 {
    string s = "I'm a string!";
    func(s); // Outputs: string value is I'm a string
    printf("string is %s\n", s.c_str()); // Outputs: string is I'm a string
    return 0;
 }
 
```






