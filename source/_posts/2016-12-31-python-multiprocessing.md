---
layout: post
title: "Python Multiprocessing"
date: 2016-12-31 09:37:01 -0800
comments: true
categories: python
keywords: python, multiprocessing, programming, parallel programming
description: Python Multiprocessing usage and demos
---

Python's GIL (Global Interpreter Lock) was designed to be a thread-safe mechanism, and it effectively prevents conflicts between multiple threads. GIL makes it easy to implemente multi-threading with Python. However, it also prevents Python multi-threading from utilizing the multiple cores of a computer to achieve improved execution speed. This is why using the ```threading``` module in Python won't help your program run faster through parallelism. 

The good thing is Python provides a [```multiprocessing``` module](https://docs.python.org/3.4/library/multiprocessing.html) since Python 2.6. With the ```multiprocessing``` module we can spawn subprocesses and effectively avoid some of the limitations that GIL brings, on both Unix and Windows platforms.

In this post I'll briefly introduce ```multiprocess``` module and show how it can be used for parallel programming.

# A simple example of *multiprocessing*

In the following example, we use ```multiprocessing``` module to spawn a child process from a parent process using a ```Process``` object.

```
from multiprocessing import Process
import os
import time

def task(name):
    print("Starting child process with id: ".format(os.getpid()))
    print("Parent process: ".format(os.getppid()))
    print("Task start: just sleeps 5 seconds ...")
    time.sleep(5)
    print("Task done")
    
if __name__ == "__main__":
    print("In parent process, id: ".format(os.getpid())
    p = Process(target=task, args=('firstone'))
    p.start()
    print("In parent process, after child process start")
    print("parent process about to join child process")
    p.join()
    print("In parent process, after child process join")
    print("parent process exiting with id ".format(os.getpid()))
    print("the parent's parent process: ".format(os.getppid()))
    
```

The output of this program will be:

```
In parent process, id 5245
In parent process, after child process start
parent process about to join child process
Starting child process with id: 5246
Parent process: 5245
Task start: just sleeps 5 seconds ...
Task done
In parent process, after child process join
parent process exiting with id 5245
the parent's parent process: 5231
```

The program starts the subprocess using ```p.start()```

# Three ways to start a process

Depending on the platform, ```multiprocessing``` supports three ways to start a process.

* __spawn__

Available on both Unix and Windows. The default on Windows. The parent process starts a fresh python interpreter process. Slower comparing with ```fork``` or ```forkserver```.

* __fork__

Parent process uses ```os.fork()``` to fork the Python interpreter. The child process is identical to the parent process, with inheritating all resources of the parent process. Available on Unix only. The default of Unix.

* __forkserver__

Starts a server process. Whenever a new process is needed, the parent process connects to the server and requests that it fork a new process. Available on Unix.

To select a start method, you can use ```set_start_method()```. This method should be used only once in the program.

```
mp.set_start_method('spawn')
p = mp.Process(target=foo, args=())
p.start()
p.join()
```

# Two ways to exchange objects between processes

Two types of communication channel between processes are supported in ```multiprocessing```, and they are: 

* class Queue
* function Pipe()

If you need know more details, the Python document [here](https://docs.python.org/3.4/library/multiprocessing.html#exchanging-objects-between-processes) will provide help.

# Use a pool of workers

The ```Pool``` class is a quite useful one in the ```multiprocessing``` module, as in real life you'll often need multiple workers to execute the tasks in your program in parallel. What the ```Pool``` class represents is a pool of workers. The following example shows how to create a pool with 4 processes as workers, and assign tasks to the workers.

```
from multiprocessing import Pool
from time import sleep

def f(x):
    return x*x

if __name__ == "__main__":
    # start 4 worker processes
    with Pool(processes=4) as pool:
        res = pool.apply_async(f, [10])
        print(res.get(timeout=1))

    pool.close()
    pool.join()
    
```

The ```apply_async(f, args, kwargs)``` method calls a function for many times, or calls a number of different functions asynchronously with arguments arguments. Each process will NOT block other processes. The order of the multiple processes are not guaranteed.

The ```close()``` prevents any more tasks from being submitted to the pool. Once all the tasks have been completed, the worker process will exit. 

The ```join()``` method waits for the worker processes to exit. It is required to call ```close()``` or ```terminate()``` before using ```join()``` method.

Both ```close()``` and ```terminate()``` will stop all the worker processes. The difference is ```close()``` will wait for worker process to finish, and ```terminate()``` immediately shut down worker processes without completing outstanding work.

Another useful method provided by ```multiprocessing``` module is ```cpu_count()```, which returns the number of CPUs in the current system. You can use this value to decide how many processes to create in a pool.


*This post is my last post in 2016. Happy new year!*




