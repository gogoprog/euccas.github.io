---
layout: post
title: "Effective Traditional C++ (3): String"
date: 2017-02-27 20:39:46 -0800
comments: true
categories: C++
keywords: C++
description: C++ string, C string, STL string
---

Recently I spent a whole lot of time on file compression and decompression with zlib. Thought I'd better write something about it. But before that, let me finish the series of "Effective Traditional C++". Today I'll write about Strings in C++. 

Two types of String are available in C++: C-Strings (C-style Strings), and STL Strings.

# C-String

C-String is a fundamental type in C++. Comparing to STL String, C-String is small, simple and fast. A C-String is a special case of an array of characters terminated with a 0. This is sometimes called an null-terminated string. A C-String can be printed out with a <code>printf</code> statement using the <code>%s</code> format string. We can access the individual characters in a C-String just as we do in an array.

<!--more--> 

**Example: print a C-String with %s**

```
char s[] = {'s', 't', 'r', 'i', 'n', 'g', 0};
printf("String is: %s\n", s);
// output:  String is: string
```

**Example: access characters of a C-String**

```
char s[] = {'s', 't', 'r', 'i', 'n', 'g', 0};
for (int i = 0; s[i]; i++)
{
    printf("Char is: %c\n", s[i]);
}
// output:
// Char is: s
// Char is: t
// Char is: r
// Char is: i
// Char is: n
// Char is: g
```

**Example: access characters of a C-String, using a pointer**

```
char s[] = "string";
for (char* cp = s; *cp; ++cp)
{
    printf("Char is %c\n", *cp);
}
// output:
// Char is: s
// Char is: t
// ... ... 
// Char is: g
```

**Example: access characters of a C-String, C++ 11 style**

In C++ 11, a *range based loop* can be used to access arrays and also C-Strings.

```
char s[] = "string";
for (char c : s)
{
    printf("Char is %c\n", *cp);
}
// output:
// Char is: s
// Char is: t
// ... ... 
// Char is: g
// Char is:
```

You may have noticed that the <code>null</code> character in the end of the C-String was printed out in the above code snippet. This is because the *range based for loop* in C++ 11 looks at the entire array and doesn't treat the <code>null</code> as the end of the C-String. To get rid of the ending <code>null</code> character in a C-String, we need add a condition checker inside the range based loop.

```
char s[] = "string";
for (char c : s)
{
    if (c==0) break;
    printf("Char is %c\n", *cp);
}
// output:
// Char is: s
// Char is: t
// ... ... 
// Char is: g
```

# STL String

The STL String class is a special type of container designed to operate with sequence of characters. It's designed with many [features and available functions](http://www.cplusplus.com/reference/string/string/) to operate on strings efficiently and intuitively. To use STL String, you need include <code>string</code> header. The following example shows the basic usage of STL string including getting the length of a string, string concatenation, comparison, and accessing each character. 
 
```
include <iostream>
include <string>
  
int main(int argc, char** argv) {
    string s0 = "Hello";
    
    // size == length
    cout << "size of string: " << s0.size() << endl;
    cout << "length of string: " << s0.length() << endl;
    // output:
    // 5
    // 5
    
    // + concatenation
    cout << "concatenated strings: ";
    string s1 = "another hello";
    cout << s0 + ", " + s1 << endl;
    // output:
    // Hello, another hello
    
    // compare: ==, >, <, >=, <=, !=
    cout << "is s0 == s1? " << (s0 == s1 ? "yes" : "no") << endl;
    s1 = s0
    cout << "is s0 == s1? " << (s0 == s1 ? "yes" : "no") << endl;
    // output:
    // no
    // yes
    
    // access each character
    cout << "each character: ";
    for (char c : s0) {
       cout << c << ' ';
    }
    cout << endl;
    // output:
    // Hello
}
```



