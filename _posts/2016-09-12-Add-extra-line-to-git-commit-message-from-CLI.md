---
layout: post
title: "Add extra line to git commit message from CLI"
author: evanbrodie
date: 2016-09-12T21:12:35+00:00
---

You can add extra lines to your commit messages by adding an extra `-m` flag to the `git commit` flag. This is useful if you have extra information that you want captured in your commit, but you don't want it in your commit message header. For example:

```
git commit -am "Updates the README with copyright information" -m "This conforms to requirements from Legal."
```

Will produce the following commit message:

```
Updates the README with copyright information

This conforms to requirements from Legal.
```

Now your commit message is split up into a **header** and a **body**. You can also add another `-m` flag for a **footer**.
