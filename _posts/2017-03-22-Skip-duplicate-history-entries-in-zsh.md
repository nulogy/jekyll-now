---
layout: post
title: "Skip duplicate history entries in zsh"
author: maksimbezsaznyj
date: 2017-03-22T19:32:40+00:00
---

In zsh, pressing UP searches through the history and brings up all matching commands, even if they are duplicates. That means, sometimes you need to press UP many times to actually find a previous match.

However, it is possible to disable this behaviour and skip duplicate entries from the history. To do that, add one line to your `~/.zshrc`:  
`setopt HIST_FIND_NO_DUPS`

