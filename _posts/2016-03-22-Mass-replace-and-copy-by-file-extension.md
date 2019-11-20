---
layout: post
title: "Mass replace and copy by file extension"
author: clemenspark
date: 2016-03-22T20:55:59+00:00
---

Problem
-----

I just cloned a Rails project.
There are a bunch of files with the `.yml.sample` extension under the config directory.

I'd like to copy all those files without the `.sample` prefix.

Solution
----

zsh functions to the rescue!

Add this to your `.zshrc` file:

```
autoload -U zmv
```

Then run:

```
zmv -C 'config/(*.yml).sample' 'config/$1'
```

By default, zmv will move files.
`-C` puts it in copy mode.

For more info:

```
man zshcontrib
```
