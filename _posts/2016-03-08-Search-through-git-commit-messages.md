---
layout: post
title: "Search through git commit messages"
author: cameronwoloshyn
date: 2016-03-08T20:37:12+00:00
---

## Problem:
How do you find the commits associated with a specific story?

## Context:
At Nulogy, we use a story tracking system that assigns a number to each story.
When we're developing, we tag each commit message with the story number: 

```
$ git commit -m "#1234 - refactors spec"
```

## Solution:
We can use `git log --grep`, which greps the commit messages in the repo: 

```
$ git log --grep="#1234"
```
