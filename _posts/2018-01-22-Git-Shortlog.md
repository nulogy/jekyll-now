---
layout: post
title: "Git Shortlog"
author: jasonschweier
date: 2018-01-22T16:31:44+00:00
---

There are many ways to customize your `git log` output. However, the structure still the same: commit by commit.

A new variation I recently discovered was `git shortlog`. It displays commits by author, rather than most recently committed order. It is intended to help producing release notes.

This lets you find out who your largest contributors are, especially with the `--summary` option. 

Try this:

```bash
$ git shortlog --summary | sort -r
```
