---
layout: post
title: "CPU Profiling Tools on Linux"
date: 2017-08-27 14:23:21 -0700
comments: true
categories: Linux 
keywords: Profiling Profiler Performance GCC
description: Review CPU profiling tools on Linux, including perf, gprof, valgrind, and google gperf tools.
---

Profiling is an effective method to provide measurements for the performance of software applications. With profiling, you get fine grained information for the components of an application, such as how often a function is called, how long a routine takes to execute and how much time are spent of different spots in the code. With these information, you could identify the performance bottlenecks and the poorly implemented parts in a software application, and find effective methods to improve them.
 
 In this post I'll write a brief summary of two profiling methods: **Instrumentation** and **Sampling**, and four CPU profiling tools on Linux: **perf**, **gprof**, **Valgrind** and Google's **gperftools**. 
 
 # Profiling Methods
 
 Different profiling methods use different ways to measure the performance of an application when it is executed. **Instrumentation** and **Sampling** are the two categories that profiling methods fall into.
 
 ## Instrumentation
 
 Instrumentation method inserts special code at the beginning and end of each routine to record when the routine starts and ends. The time spent on calling other routines within a routine may also be recorded. The profiling result shows the actual time taken by the routine on each call. 
 
 There are two types of instrumenting profiler tools: **source-code modifying** profilers and **binary profilers**. Source-code modifying profilers insert the instrumenting code in the source code, while the binary profilers insert instrumentation into an application's executable code once it is loaded in memory. 
 
 The good thing of instrumentation method is it gives you the actual time. The inserted instrumentation code (timer calls) take some time themselves. To reduce the impact of that, at the start of each run profilers measure the overhead incurred from the instrumenting process, and later subtract this overhead from the measurement result. But the instrumenting process could still significantly affect an application's performance in some cases, for example when the routine is very short and frequently called, as the inserted instrumentation would disturb the way the routine executes in the CPU.
 
 ## Sampling
 
 Sampling measures applications without inserting any modifications. Sampling profilers record the executed instruction when the operating system interrupts the CPU at regular intervals to execute process switches, and correlates the recorded execution points with the routines and source code during the linking process. The profiling result shows the frequency with which a routine and source line is executing during the application's run. 
 
Sampling profilers causes little overhead to the application run process, and they work well on small and often-called routines. One drawback is the evaluations of time spent are approximations instead of actual time. Also sampling could only tell what routine is executing currently, not where it was called from. As a result, sampling profilers can't report call traces of an application. 

# CPU Profiling Tools on Linux

## perf

The [```perf```](https://perf.wiki.kernel.org/index.php/Main_Page tool is provided by Linux kernel (2.6+) for profiling CPU and software events. To use it, you can do the installation as:

- Ubuntu: install *linux-tools_common*
- Debian: install *linux-base*
- Arch: install *perf-utils*
- Fedora: install *perf*

```perf``` is based on the perf_events system, which is based on event-based sampling, and it uses CPU performance counters to profile the application. It can instrument hardware counters, static tracepoints, and dynamic tracepoints. It also provide per task, per CPU and per-workload counters, sampling on top of these and source code event annotation. It does *not* instrument the code, so that it has a really fast speed and generates precise results. 

 You can use ```perf``` to profile with ```perf record``` and ```perf report``` commands:
 
 ```
 perf record -g <app> <options>
 perf report
 ```

The ```perf record``` command collects samples and generates an output file called ```perf.data```. This file can then be analyzed using ```perf report``` and ```perf annotate``` commands. Sampling frequency can be specified with ```-F``` option. As an example, ```perf record -F 1000``` means 1000 samples per second.

## gprof



## Valgrind

## gperftools


 
 