---
layout: post
title: "Searching Through Gems"
author: jasonschweier
date: 2018-01-17T14:55:41+00:00
---

Sometimes you need to peak at the source of a class or method of a gem from your `Gemfile`. Since gems are managed by [`bundler`](http://bundler.io/), it has a command-line option that can help.

`bundle show --paths` will list the paths of all the gems from your `Gemfile`. You can grep through these directories to search.

I'm currently using [ripgrep](https://github.com/BurntSushi/ripgrep) for searching at the command line, so can pass the paths there.

Here’s it all together in a simple Bash function:

```bash
function bundle-search() {
	rg $1 `bundle show --paths`
}
```
