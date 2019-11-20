---
layout: post
title: "Learning lessons the hard way: git clean"
author: jordanneville
date: 2016-05-17T20:03:26+00:00
---

I had a huge list of superfluous changes in git that I wanted to clean up. Most of them were additions so doing a `git checkout` wasn't going to work.

I followed some instructions online and ran: `git clean -r -d -x`

The trojan horse of this command is the `-x` flag which will **delete all files in your .gitignore!** 

This led to a half day of setting up my dev environment again to recover all the lost environmental configurations deleted by this command. 

Stay tuned for tomorrow's lesson: *Adventures with `rm -rf /`*
