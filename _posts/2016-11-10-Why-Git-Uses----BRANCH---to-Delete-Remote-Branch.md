---
layout: post
title: "Why Git Uses (:<BRANCH>) to Delete Remote Branch"
author: shahriyarnasir
date: 2016-11-10T22:16:56+00:00
---

It would appear that the colon in `git push origin :<branch-to-delete>` is used exclusively to delete branches. But such is not the case.

The format for the refspec is*:

```
<source>:<destination>
```

This tells Git to push the `source` branch to the `destination` branch in remote. So if the `source` is blank, we get a leading colon. This has the *effect* of deleting the `destination` branch. Its like saying "push null pointer to destination".

*You can learn more about the refspec in its entirety in [this](http://stackoverflow.com/questions/7303687/why-git-use-the-colon-branch-to-delete-remote-branch) Stack Overflow
