---
layout: post
title: "Diffing a topic branch against the base branch"
author: clemenspark
date: 2016-04-05T21:38:16+00:00
---

I often want to check all the changes made in my branch, relative to the base branch.
Let's say the base branch is master.

Most of the time, I use plain ol' `git diff`.

```
git diff master
git diff master --name-only  # only list the changed files
```

However, `git diff master` doesn't always work.  For example, if I pulled the latest changes in master, and haven't rebased my branch, then `git diff master` will show all kinds of changes I didn't make.

So what is a dev to do?

`git merge-base` to the rescue!

Here's the description from `git help merge-base`:

    Find as good common ancestors as possible for a merge

The following gives me a good commit to compare against:

```
> git merge-base master HEAD
0783e77e5ca810e36fc7080753ac62526c09d0e4
```

Therefore, I can check all my changes using:

```
git diff `git merge-base master HEAD`
```

zsh function:

```zsh
gdb() {
  git diff `git merge-base master HEAD` $@
}
```
