---
layout: post
title: "Attach to Local Ruby Process with Debugger"
author: arturopie
date: 2016-12-11T20:33:09+00:00
---

RubyMine has a nice feature that allows you to debug a Rails app without restarting the server.

With the server running, 

1)  Run the "Attach to Local Process.." action from RubyMine

2)  RubyMine will show a list of Ruby processes running. Pick the one running your server

3) Wait for RubyMine to connect to the process

4) Add a break point in RubyMine

5) Execute the action on the web application that hits that breakpoint

6) Execution will stop on that line. Now you can use all the nice tools the RubyMine debugger gives you.

I'm really exited with this new feature and I hope you are too. You can read more about it in [here](https://blog.jetbrains.com/ruby/2016/11/attach-to-local-process-with-debugger)

![RubyMine Attaches to Local Ruby Process ](https://www.jetbrains.com/ruby/whatsnew/screenshots/2016.3/attach_to_local_process.gif)
