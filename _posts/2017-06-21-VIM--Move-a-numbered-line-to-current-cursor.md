---
layout: post
title: "VIM: Move a numbered line to current cursor"
author: evanbrodie
date: 2017-06-21T19:38:38+00:00
---

Let's say I'm on line 20 and I want to move line 10 to my current line. Useful for code refactoring.

## How I used to do it

```
10G
dd
19G
p
```

Or:

```
:10d
p
```

## The new way I'll do it

Thanks to my learnings [here](http://vim.wikia.com/wiki/Moving_lines_up_or_down#Move_command):

```
:10m .
```
