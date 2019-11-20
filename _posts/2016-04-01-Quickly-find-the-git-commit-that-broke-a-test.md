---
layout: post
title: "Quickly find the git commit that broke a test"
author: arturopie
date: 2016-04-01T13:22:46+00:00
---

Git bisect is a very cool tool that automate a binary search for you to find the first "bad" commit.
Here is an example on how to find a commit that broke a test:

1. `git bisect start`
2. `git bisect good <good_sha>     # <good_sha> is any commit where the test is passing `
3. `git bisect bad <bad_sha>          # <bad_sha> is any commit where the test is failing`
4. `git bisect run zeus rspec <broken test>  # remove zeus if you don't use it`

Git bisect will perform a binary search and run the test on every step. It uses rspec exit status to know if the commit is "good" or "bad" (0 exit status means "good", otherwise it's "bad"). When it's done it will print the first bad commit:

```
a5cf29ac1dd64e5ce05336f28aa0ffc17e57fc10 is the first bad commit
commit a5cf29ac1dd64e5ce05336f28aa0ffc17e57fc10
Author: Arturo Pie <example@example.com>
Date:   Fri Apr 1 08:55:31 2016 -0400

    This is the commit message

:040000 040000 b2399ed1361548a743d95aa6aa95e42096f5ffd3 b500421bbfb9bb3dfebee1e45ff2197a7f32a43e M	app
bisect run success
```

When you are done debugging, run `git bisect reset` to end the bisect.

Happy Hacking!
