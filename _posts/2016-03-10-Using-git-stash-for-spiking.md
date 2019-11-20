---
layout: post
title: "Using git stash for spiking"
author: clemenspark
date: 2016-03-10T19:02:04+00:00
---

Often, I do a small spike to see if a certain code change makes sense.
When it's time to actually make code changes, I want to start from scratch to do proper TDD.
However, sometimes I want to reference the code I spiked out to guide me. 

One option is to stash away the spike, and reference it using:

```
git stash show -v
```

This will show you the contents of the most recently stashed code.

If it's not the most recently stashed change, you can specify the stashed change you want to see:

```
git stash list
git stash show -v @{2}
```
