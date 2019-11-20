---
layout: post
title: "Force push safely using --force-with-lease"
author: bryanmacdiarmid
date: 2017-11-14T20:20:08+00:00
---

We periodically force push feature branches when we rebase them. 

To do this safely, I first check manually to see if my pair has pushed any commits I don't yet have in my local branch. 

But there's an easier and safer way to do this.  **The `--force-with-lease` option will fail if there are upstream changes not yet merged.**

It will work smoothly for standard rebasing situations, but protect against any inadvertent destructive force pushes.

Thanks to Jason K for sharing this tip with me!
