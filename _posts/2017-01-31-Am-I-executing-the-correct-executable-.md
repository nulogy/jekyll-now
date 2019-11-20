---
layout: post
title: "Am I executing the correct executable?"
author: clemenspark
date: 2017-01-31T20:58:12+00:00
---

Q: When I run a command (let's say rails), which executable is it executing?

A:

    > which rails
    /Users/username/.rvm/gems/ruby-2.1.6/bin/rails
    
Q: Ah, I see which one it's running. And it's not the right one! Where are all the potential executables, given the current PATH?

A:

    > where rails
    /Users/username/.rvm/gems/ruby-2.1.6/bin/rails
    /usr/bin/rails

Now I know whether it's a PATH ordering issue, or whether it's not included PATH at all.
