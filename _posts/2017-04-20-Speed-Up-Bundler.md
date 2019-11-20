---
layout: post
title: "Speed Up Bundler"
author: alistairmckinnell
date: 2017-04-20T10:55:35+00:00
---

It turns out that you can speed up [Bundler](http://bundler.io/v1.14/man/bundle-install.1.html) if you increase parallelization.

````
$ bundle config --global jobs 8
````

On OS X you can use the `sysctl` command to determine the `jobs` setting appropriate for your hardware:

````
$ sysctl hw.ncpu
hw.ncpu: 4
````

I'm using [number of cores times two](http://blog.mroth.info/blog/2014/10/02/rubygems-bundler-they-took-our-jobs/). Works for me. YMMV.
