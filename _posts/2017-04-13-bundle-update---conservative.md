---
layout: post
title: "bundle update --conservative"
author: bryanmacdiarmid
date: 2017-04-13T02:47:28+00:00
---

Let's say you want to update the gem foo. After running `bundle update foo` you look at your gemfile.lock and find that not only was foo updated, but so were many of its dependencies. You also notice that many of these dependency updates weren't necessary, as the previously installed versions were compatible with the new version of foo.

The default `bundle update foo` behaviour will unlock and update all dependencies of foo.

If you don't want to update these dependencies unnecessarily, one solution is to add the current versions to your gemfile.lock.

However, an easier way to prevent the updating of shared dependencies is to use bundler's new `--conservative` flag. 
