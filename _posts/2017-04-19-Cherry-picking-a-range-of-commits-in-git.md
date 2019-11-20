---
layout: post
title: "Cherry-picking a range of commits in git"
author: ryandevilla
date: 2017-04-19T15:18:42+00:00
---

# Problem

I would like to cherry-pick a range of commits (e.g. an entire branch). For example, I want to cherry-pick the commits `f00b4r` to `f00ba5`, where `foob4r` is the oldest commit on the branch.

# Solution

`git cherry-pick f00b4r~..f00ba5`.
