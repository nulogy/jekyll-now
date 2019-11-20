---
layout: post
title: "Ignore whitespace-only changes in Gitlab MRs"
author: evanbrodie
date: 2017-03-22T16:28:08+00:00
---

## Problem

You are reviewing a Gitlab Merge Request (MR). It involes changes where a Ruby file is moved into or out of particular modules. This means that one or more `module ... end` constructs are either added or removed around the entire class, resulting in a tabbing-width change on almost every line of the file. This makes reviewing the file in the MR quite difficult, as the reviewer will need to sift through the code diff and separate out actual logic changes from whitespace-only changes.

## Solution

By appending `?w=1` to the end of the URL of the MR, Gitlab will ignore all lines that only feature a whitespace change in the code diff. This means that the only changes visible will be ones with a non-whitespace change, thus allowing the reviewer to focus in on actual logic changes and not waste time reading whitespace changes.

Time to poke Gitlab EE support on this issue: https://gitlab.com/gitlab-org/gitlab-ce/issues/1393
