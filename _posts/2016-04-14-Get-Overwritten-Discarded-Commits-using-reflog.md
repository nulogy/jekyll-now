---
layout: post
title: "Get Overwritten/Discarded Commits using reflog"
author: joneriksuero
date: 2016-04-14T20:04:20+00:00
---

```
git reflog
```
shows commits including the overwritten/discarded ones. This is useful in case of accidents such as unwanted `git commit --amend` and `git reset`.

Source
===
https://www.atlassian.com/git/tutorials/rewriting-history/git-reflog

Extra
===
Use
```
git reflog --date=iso
```
to include dates.
