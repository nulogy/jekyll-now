---
layout: post
title: "What's a \"twiddle-wakka\"?"
author: evanbrodie
date: 2016-04-14T21:25:44+00:00
---

I'm proud to say that I now know what a "twiddle-wakka" is. It is the notation `~>` that we use in our Ruby-flavoured semver notation in Gemfile. Specifically, it means that the accepted version must be at the *same level* of the specified version. All sub-levels below the next increment of the current level are accepted. For example, `~> 2.0` means `2.0 <= VERSION < 2.1`, while `~> 2.0.1` means `2.0.1 <= VERSION < 2.0.2`.

Reference: http://guides.rubygems.org/patterns/

But seriously, now I know what a "twiddle-wakka" is. :D
