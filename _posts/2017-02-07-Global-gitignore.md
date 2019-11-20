---
layout: post
title: "Global gitignore"
author: diogobiazus
date: 2017-02-07T20:16:16+00:00
---

To enable a global **.gitignore** for a specific user you can use the git config **core.excludefiles** as in:

    git config --global core.excludesfile '~/.gitignore'

This will make the **.gitignore** in your home folder to be used in every git project in adition to local **.gitignore** files.

For more info read the [git documentation on gitignore](https://git-scm.com/docs/gitignore)
