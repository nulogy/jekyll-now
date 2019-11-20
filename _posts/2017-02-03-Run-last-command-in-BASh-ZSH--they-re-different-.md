---
layout: post
title: "Run last command in BASh/ZSH (they're different)"
author: evanbrodie
date: 2017-02-03T20:10:59+00:00
---

To run the last executed command in BASH, execute the following:

```sh
!!
```

In ZSH, things are a little different. Using `!!` will only expand the command into the shell prompt. You would have to press enter again to execute it. Rather, if you want to immediately execute the last command similar to BASH, use this:

```sh
r
```

If you prefer for ZSH behaviour to match that of BASH, then add `setopt no_hist_verify` to your *.zshrc* file.
