---
layout: post
title: "the elements of linux screen"
date: 2014-05-31 14:51:54 -0700
comments: true
categories: linux
---

The Element of Linux Screen

[Linux Screen](http://aperiodic.net/screen/start) is a tool installed in Linux system with which you can manage multiple interactive shell processes. With Screen, you can have multiple shells in the same window. You can detach shell processes and attach them when you log into the system from other sessions. With Screen, you don't need worry about losing your half-way tasks when the terminal exit. I use the Screen on a daily basis, and here I write down the commands and usages that are most commonly used in my everyday work.
 
 
#  Start Screen
 
In a system where screen is installed, type "screen" in a terminal will invoke it.

If screen isn't installed in your system, Google "install screen in Linux" to find the solution.

<!--more--> 
 
Screen can also has a **session name** when get started:

 `screen -S`

If no session name is specified, screen will use the default Shell name as the session name.

Example:

    Num  Name
    0	bash
    1	bash
 
# Do some configurations
Screen uses a configuration file "~/.screenrc". It could be empty if there is no customized configurations.

You can skip this .screenrc config and use everything set as default by Screen. It will be fine most of the time. However if you use **Emacs**, you might need **change the default command key** used by Screen in the .screenrc file. Here is the why and how.
 
Command key in Screen means the key input that issues the commands to Screen instead of to Linux shell.
By default, the Screen command key is `Ctrl+A` (C-A).
 
    C-A ? : show the key binning used by Screen
 
Emacs also uses C-A as the command key, so you may face the command key conflict when using Emacs in Screen. To make sure the command key work properly when use Screen and Emacs together, change the command key of Screen in .screenrc to be a command that not used by Emacs.
 
Some examples:

    ~/.screenrc$
    
    escape ^L^L   #use Ctrl+L
    escape ^^^^   #use Ctrl+^
    escape ^]^]   #use Ctrl+]
 
Note the first "^" means command key, the second "^" means literal insert key.

You can also set the default caption names when you have multiple shells in one screen

    ~/.screenrc$

    caption always "%{= kw}%-w%{= BW}%n %t%{-}%+w %-= @%H - %LD %d %LM - %c"
 
# Common Screen Commands

## From Linux Shell ##

    screen  	# start a screen
    screen -S   # start a screen with a session name
    screen -ls  # list current screens
    screen -d  	# detach the current screen
    screen -r  	# re-attach the screen that was attached

## From Screen ##

    C-a " 		# list all interactive shells
    C-a c  		# create a new interactive shell (window)
    C-a k  		# kill the current window
    C-a n (or ) # switch to the next shell window
    C-a p (or )	# switch to the previous shell window
    C-a shift-A  # rename current window
    C-a S  		# split display horizontally
    C-a V  		# split display vertically
    C-a tab		# jump to the next display region
    C-a X  		# remove current region
    C-a Q  		# remove all regions but the current one 
 
When split the windows horizontally, use `C-a S`.
Then use `C-a tab` to move between the horizontally split regions.
 
 
`screen -S SESSIONNAME` is good for starting a session with a name, but if you start a session and later decide to name it or rename it, you'll need enter command mode `(C-a :) `and then enter the command `sessionname SESSIONNAME`.
 
These are all my notes for using Linux Screen. Hopefully it could help you use it better!