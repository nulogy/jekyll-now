---
layout: post
title: "How to view changes from only a particular branch"
author: evanbrodie
date: 2016-03-15T18:20:43+00:00
---

`git log master..`, assuming your branch was based off of master. If based off of something else, use that branch name (ie, `git log production..`)

Courtesy of http://stackoverflow.com/a/4649377/814576
