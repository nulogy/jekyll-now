---
layout: post
title: "RubyMine group search by Test and Production code"
author: evanbrodie
date: 2016-06-07T18:14:19+00:00
---

When I do code searches in RubyMine, I sometimes want to only see non-test code for various reasons, such as knowing how often a particular method is used in our code base to judge adoption level. Normally, I would have to select each directory and run a code search one at a time, or search all directories at once and carefully skip over all test code while scrolling through the list. In a Rails app, directories that contain non-test source code could include `app/`, `domain/`, `lib/` and even more.

There is a better way! The RubyMine Search tab has a toggle that will let you group source code search by Production and Test code. All you have to do is press [this toggle](http://i.imgur.com/yhROwFm.png) and voila!
