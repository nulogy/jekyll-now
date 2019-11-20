---
layout: post
title: "Removing untracked files/directories in git"
author: hasithapathiraja
date: 2016-03-09T18:07:39+00:00
---

To remove untracked files/directories, use **git-clean**.

Running git-clean prints out what it would remove, without actually removing them.

-f flag removes the files and -d flag removes empty directories

So to remove untracked files and directories:

```
git clean -df
```

To also remove ignored files:

```
git clean -dfx
```
