---
layout: post
title: "Passing all env. variables to a shell command"
author: arturopie
date: 2016-12-16T16:55:55+00:00
---

Some of the methods in the [Kernel](https://ruby-doc.org/core-2.2.0/Kernel.html#method-i-system) module  allows you to pass environment variables to a shell command. So rather than doing:

    system("RAILS_ENV=test rake do_stuff")

You can do 

    system({ "RAILS_ENV" => "test" }, "rake do_stuff")  

This is particularly useful when we want to pass all environment variables on our current process.

    system(ENV, "rake do_stuff")


