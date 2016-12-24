---
layout: post
title: "Levels of Design"
date: 2016-12-24 09:52:07 -0800
comments: true
categories: system-design algorithm
---

I'm taking a course ["Algorithm Toolbox"](https://www.coursera.org/learn/algorithmic-toolbox/home/welcome) on Coursera recently. This course provides me a good chance to review and enhance my knowledge in the fundamental algorithms, which usually would help on achieving better system design. This morning I came across one slide of this course and thought it could be very useful. Sharing it here.

{% img center /images/post_images/20161224-levels-of-design-1.png %}

It's important to keep the levels of (algorithm) design in mind when solving a problem. 

* Level 1: Naive Algorithm

This is the solution that you can get just by taking the definition of a problem and turning it into an algorithm. This solution can solve the problem, but it is often very slow and inefficient. 

The way I see the naive algorithm is it gives you something that works, and might be used to verify if alternative solutions are correct or not. But it's important to not stay at the this solution. You should keep looking for better solutions.

* Level 2: Algorithm by way of standard Tools

You can look at the standard techniques and see if any of it applies to solving your problem. On this level, your goal is finding some standard techniques that work, often that don't involve too much effort on your part, and give you something that work very well (better than the naive algorithm). 
 
* Level 3: Optimized Algorithm

Remember there are always lots of ways to improve an existing solution. If you get a pretty good solution on level 2, why not taking one more step and see what you can do to improve it? Could you reduce the runtime from n-cubed to n-squared or n-squred to n? Could you come up with a shorter solution by rearranging the order or cut out some of the work? Could you use a data structure to speed things up? Think about all these possiblities and see if you can get a even better solution. (Often you will) 

* Level 4: Magic Algorithm

When the solutions from the previous three levels are not good enough, you'll need some magic to get a better one. This can be hard. You will need some clever new ideas and unique insights of the problem you're trying to solve. Even if you don't get a magic solution in the end, the thought process will be beneficial.

Sometimes when I finish a project, I do have the feeling that the way I do it is just not good enough, even though the project has been proved to be successful, useful and solved a particular technical challenge we faced. Looking at the "Levels of Design", I believe what I need to do is spending more efforts on the higher levels. Actually what you really need for getting a really good solution is not magic. What you need is mastering more existing good standard techniques, exploring the possibility for optimization, and a deep understanding of the problem you want to solve. 

 
 

