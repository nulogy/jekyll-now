---
layout: post
title: "Rebase your branch from one branch to another"
author: arturopie
date: 2018-08-16T18:25:41+00:00
---

Use: `git rebase --onto new-base-branch current-base-branch`

For example, let's say we have a feature branch based on master, and we decided it's better to rebase it off production. This is our current git history:

```
commit 6 [my-feature-branch]
commit 5
commit 4 [master]
commit 3
commit 2 [production]
commit 1
```

We just need to run:

```````
git checkout my-feature-branch
git rebase --onto production master
````

And we will end up with the following history:

```
commit 6 [my-feature-branch]
commit 5
commit 2 [production]
commit 1
```

Reference: https://makandracards.com/makandra/10173-git-how-to-rebase-your-feature-branch-from-one-branch-to-another
