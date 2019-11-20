---
layout: post
title: "Finding a Rake Task Definition"
author: alistairmckinnell
date: 2019-06-04T18:20:31+00:00
---

Suppose you use a certain Rake task. Is there an easy way to find out where that task is defined?

There is. Use the ` --where` option. 

Example: `rake --where packman:update`
