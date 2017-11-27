---
layout: post
title: "How Instagram moved to Python 3"
date: 2017-06-16 17:52:34 -0700
comments: true
categories: Python Infrastructure System-Design
keywords: python python3 instagram infrastructure
description: How Instagram moved to Python 3, the challenges and problem solved when migrating to Python 3
---

Instagram, the famous brunch sharing app, presented in [PyCon 2017](https://us.pycon.org/2017/) and gave a talk in the keynote session on "How Instagram moves to Python 3". If you have 15 minutes, read the interview with the speakers, Hui Ding and Lisa Guo from Instagram Infrastructure team, [**here**](https://thenewstack.io/instagram-makes-smooth-move-python-3/]). If you have 45 minutes, watch their PyCon talk video, [**here**](https://www.youtube.com/watch?v=66XoCk79kjM). If you have only 5 minutes, continue reading, **right here**.

Instagram's backend, which serves over 400 million active users every day, is built on Python/Django stack. The decision on whether moving from Python 2 to Python 3, was really a decision on whether investing in a version of the language that was mature, but wasn't going anywhere (Python 2 is expected to retire in 2020) -- or the language that was the next version and had great and growing community support. The major motivations behind Instagram's migration to Python 3 are:

- **Typing support** for dev velocity
- Better **performance** than Python 2
- **Community** continues to make Python 3 better and faster

The whole migration process took about 10 months, in roughly 3 stages.

<!--more--> 

{% img center /images/post_images/2017/20170616-instagram_python3_00.png 520px %}

- First off, the migration was done directly on the Master Branch, which means the developers were adding new features to the code while migration was ongoing. So in the beginning of the Mirgration process, infrastructure added support of Python 3 on the Master Branch to make the code be able to run with both Python 2 and Python 3 environment. 
- Massive code modification for 3 months, with the help of Python package [**"modernize"**](https://pypi.python.org/pypi/modernize). Meanwhile, upgraded Third-party packages to Python 3 (working rule: *No Python 3, no new package*). Also deleted unused, incompatible packages.
- Intensive unit testing for 2 months. One limitation is data compatibility issues typically do not show up in unit tests.
- Production rollout for another 4 months (push Python 3 to every developer's sandbox)

In the talk, Lisa shared the challenges they faced in the migration process and how did they solved those problems.

- Differences in **unicode**, **str**, **bytes**. Solved by using helper functions.
- **Pickle memcache data format incompatibility** in Python 2 and Python 3. Solved by isolating memcaches for Python 2 and Python 3.
- **Iterator** differences, such as ```map```. Solved by converting all maps to list in Python 3.
- **Dictionary order** is different in different Python versions, which caused differences in the dumped JSON data. Solved by forcing ```sorted_keys``` in ```json.dump``` function.
- With Python 3, while CPU instructions per request decreased by 12%, max requests per second (capacity) had 0% increase! Found the root cause in the code of checking memory configuration, and the issue was memory optimization condition was never met in Python 3 as ```True``` because of unicode issue. Solved by adding a magical character **"b"**, just like this:

{% img center /images/post_images/2017/20170616-instagram_python3_01.png 520px %}

In Feb 2017, Instagram's stack completely dropped Python 2 and moved to Python 3 (v3.6). So far they've got this from Python 3:

{% img center /images/post_images/2017/20170616-instagram_python3_02.png 520px %}

One more thing, in the talk Hui Ding also briefly discussed a few **Python Efficiency Strategies** that Instagram used to support the growing number of features and users:

- Build extensive tools to profile and understand perf bottleneck
- Proactively push stable, critical components to C/C++, e.g., memcached access library
- Use Cythonization to improve performance
- Future ideas: Make the Django stack completely Async? Create a new python runtime?

Changing an existing service to use a new version of language can never be easy, especially when your service is at such a scale - serving millions of people. You just cannot afford to breaking the existing service. Moving to Python 3 in 10 months must be a challenging process. "It can be done. It worths it. Make it happen. And Make Python 3 better."

Nice work Instagram!

{% img center /images/post_images/2017/20170616-instagram_python3_03.png 520px %}
