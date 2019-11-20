---
layout: post
title: "Add a message to git stash"
author: cameronwoloshyn
date: 2016-03-10T22:49:51+00:00
---

## Problem:
You want to stash a number of patches and add a message to describe what each includes.

## Context:
Using `git stash` without arguments stacks your code changes on the top of a the stash stack, and adds a default message: "WIP on <em>branchname</em> …​". If you stash multiple patches, you may find it difficult to recall what each stash includes: 

```bash
$ git stash list

stash@{0}: WIP on 1234_add_new_feature: 1a2b3c4 #1234 - updates new feature template
stash@{1}: WIP on 1234_add_new_feature: 1a2b3c4 #1234 - updates new feature template
```

## Solution:
You can add a message to the the stash by using the `save` argument:

```bash
$ git stash save "refactors how the UI elements are rendered"
$ git stash list

stash@{0}: On 1234_add_new_feature: refactors how the UI elements are rendered
stash@{1}: WIP on 1234_add_new_feature: 1a2b3c4 #1234 - updates new feature template
stash@{2}: WIP on 1234_add_new_feature: 1a2b3c4 #1234 - updates new feature template
```
<br />

*This workflow is especially useful when you're [stashing commits while spiking.](https://til-engineering.nulogy.com/posts/d33b7ec61f-using-git-stash-for-spiking)*
