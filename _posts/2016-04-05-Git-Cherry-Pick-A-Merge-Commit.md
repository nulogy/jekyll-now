---
layout: post
title: "Git Cherry-Pick A Merge Commit"
author: evanbrodie
date: 2016-04-05T21:28:56+00:00
---

PROBLEM
----------
I picked up work on a topic branch that has a WIP commit. I reset the branch, fix a few lines, then committed. I noticed now that I'm 1 Ahead and 1 Behind on my branch. I should do a force push....but I forgot to! Instead, I pulled and thus created a merge commit. Ruh roh!

```
                 WIP
             /        \
A --- B --- C --- D --- M --- E --- F
```

Not only will this merge commit (empty, by the way) make our overall git history look ugly, it is also going to make rebasing off master very difficult, since we will have to resolve a conflict for all future commits (E and F). I want to keep my topic branch flat.

SOLUTION
----------
You can escape this mess via a series of git cherry picks. The key part of this is how we applied the cherry-pick on merge commit F. We need to specify which "parent" to base the commit off of.

```
git checkout -b new_branch
git cherry-pick A
git cherry-pick B
git cherry-pick C
git cherry-pick D
git cherry-pick M -m 1
git cherry-pick E
git cherry-pick F
```
