---
layout: post
title: "CMake: Use the correct options to solve linker errors"
date: 2017-05-29 22:30:46 -0800
comments: true
categories: build cmake
keywords: build cmake linker
description: CMake options for linkers, difference between TARGET_LINK_LIBRARIES and LINK_DIRECTORIES
---

A few months ago when I worked on a project using zlib to compress and decompress files, I once met linker errors complaining about unable to resolve symbols of zlib functions:

```
cannot resolve symbols _gzbuffer, _gzopen, ...
```

In the end I fixed these linker errors by using ```TARGET_LINK_LIBRARIES``` command in the project's CMakefile to specify the linker package dependency, as the following:

```
TARGET_LINK_LIBRARIES(myProject zlibstatic)
```

When I was looking for solutions to fix those linker errors, I found several related CMake commands which look quite similar and could be confusing in terms of their functions and when to use them. Here is a quick summary of these commands.

Related CMake commands:
* add_dependencies
* link_directories
* link_libraries
* target_link_libraries

# ADD_DEPENDENCIES(zlibProfiler zlibstatic)

Usage: ```add_dependencies(<target> ...)```

ADD_DEPENDENCIES adds a dependency between top-level targets. It makes a top level target depend on other top level targets to ensure that the dependents build beforehand. This command doesn't ensure CMake to find the path to the targets though.

# LINK_DIRECTORIES

Usage: ```link_directories(directory1 directory2 ...)```

LINK_DIRECTORIES specifies directories in which the linker will look for libraries. This command will apply only to targets created after it is called. This command is rarely necessary. You can always pass absolute paths to target_link_libraries() command instead. 

The function of this command is similar to ```-L``` option in g++. It is also similar to adding the specified directories to environment variable ```LD_LIBRARY_PATH```. 

# LINK_LIBRARIES

Usage: ```link_libraries([item1 [item2 [...] ]])```

LINK_LIBRARIES specifies link libraries or flags to use when linking all targets added later by commands such as ```add_executables()``` or ```add_library()```. 

This command was deprecated in CMake version 3.0, and was added back in version 3.2. But CMake document recommends using ```target_link_libraries``` to replace this command whenever possible.

The link libraries specified in this command are expected to be full paths.

# TARGET_LINK_LIBRARIES

Usage: ```target_link_libraries(<target> ... <item> ...)```

TARGET_LINK_LIBRARIES specifies libraries or flags to use when linking a given target and/or its dependents. The specified target must be created by ```add_library()``` within the project or as an imported library. 
