---
layout: post
title: "Ignore some paths from git diff"
author: clemenspark
date: 2019-04-08T19:37:22+00:00
---

Problem
===

I want to do a `git diff`, but I need some paths to be ignored.

e.g. `git diff --name-only`

Output:

```
some_dir/aaa
some_dir/bbb
some_dir/ignore_me/aaa
some_dir/ccc
some_dir/ddd
```

What I want:

```
some_dir/aaa
some_dir/bbb
some_dir/ccc
some_dir/ddd
```

Solution
===

[Git pathspecs](https://git-scm.com/docs/gitglossary)!

"After a path matches any non-exclude pathspec, it will be run through all exclude pathspecs (magic signature: ! or its synonym ^). If it matches, the path is ignored."

`git diff --name-only -- '!**/ignore_me/*'`

