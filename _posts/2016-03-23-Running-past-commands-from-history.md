---
layout: post
title: "Running past commands from history"
author: jasonyuen
date: 2016-03-23T19:34:15+00:00
---

There are many ways to search/recall previous commands from the command line but I find the combination of ```history``` and ```!<history_id>``` to be quite useful, especially when you don't remember the command you ran. For example:

Show me my previous commands:

```
> history
  513  git stash pop
  514  rspec spec/some_spec.rb
  517  git diff
  518  git add -p
```

Re-run the spec command in 514

```
> !514
```

