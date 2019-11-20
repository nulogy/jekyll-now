---
layout: post
title: "Diffing code snippets between large files"
author: ryandevilla
date: 2016-03-30T13:57:07+00:00
---

Sometimes I like to compare and contrast differences between sections of large files that exhibit textual similarity.

Suppose I want to compare lines 100-200 from `FileA.txt` with lines 300-400 from `FileB.txt`. The following can be accomplished from the command line as follows:

```bash
diff <(sed -n '100,200p' /path/to/FileA.txt) <(sed -n '300,400p' /path/to/FileB.txt)
```

You can substitute `diff` with any program of your choice (try diffuse, meld, or vimdiff).
