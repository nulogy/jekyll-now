---
layout: post
title: "Stashing untracked files in Git"
author: ryandevilla
date: 2016-03-15T21:23:38+00:00
---

Scenario
--------

I have created new files in the process of spiking an implementation, and want to stash them to prevent "Untracked files" from appearing in `git status`.

Solution
--------

Use `git stash save -u`.
