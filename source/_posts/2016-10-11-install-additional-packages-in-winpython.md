---
layout: post
title: "Install additional packages in WinPython"
date: 2016-10-11 17:11:51 -0700
comments: true
categories: Python
---

For people who need use portable Python on Windows, [WinPython](https://winpython.github.io/) is a good choice. WinPython is a free open-source portable distribution of Python. The project is hosted on [github](https://github.com/winpython). It is also a good alternative to [Portable Python](http://portablepython.com/), which is not being developed anymore.

In this post I'll show you how could you install additional packages to WinPython.

# Install WinPython

WinPython is portable. It means that you can download WinPython from the [WinPython download page](http://winpython.sourceforge.net/), add it to your system PATH, and start using it without any installation.

<!--more--> 

* Unzip the downloaded WinPython Package to a local directory, eg. ```C:\WinPython```.
* Add the local directory path to your system's ```PATH``` variable. You can use Windows command ```set``` or ```setx```.

```
   set PATH=C:\WinPython\;%PATH%
```

Now you can open a Windows cmd prompt, and test your installed python version.

```
    where python
	>>> C:\WinPython\python.exe
```

# Install a package

You can install a Python Package to WinPython using ```pip```. If you have other versions of Python installed on your computer, you'll need make sure the ```pip``` you use actually is the one WinPython provides.

Where is the ```pip```? 

It's in the ```Scripts``` directory of the WinPython path.
For example:

```
C:\WinPython\Scripts
```

Now you can use the WinPython ```pip``` to install additional Python packages.


```
<WinPython Path>\Scripts\pip install <package name>
```

If the installation successfully done, you will find the installed packages in WinPython's library path.

```
<WinPython Path>\Lib\site-packages\<package name>
```

That's it! Your Python package is ready to use!









