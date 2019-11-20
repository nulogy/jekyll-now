---
layout: post
title: "Convenient Git Command to Discard Local Changes"
author: alistairmckinnell
date: 2017-01-22T19:11:20+00:00
---

In order to discard all local commits on a branch, that is, to make the local branch identical to the *upstream* of the branch, run:

``````
git reset --hard @{u}
```

where `@{u}` is the short form of `@{upstream}` and denotes the [upstream branch](https://git-scm.com/book/en/v2/Git-Branching-Remote-Branches).
