---
layout: post
title: "Speeding Up Rake Command Completion"
author: alistairmckinnell
date: 2017-03-06T20:53:40+00:00
---

The speed of `rake` command completion is determined by the startup time of your Rails app.

If your Rails app is slow to startup, the [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) [rake-fast](https://github.com/robbyrussell/oh-my-zsh/tree/master/plugins/rake-fast) plugin will make `rake` command completion tolerable again.

Edit your zsh configuration file: 

```
plugins=(... rake-fast ...)
```

After refreshing your shell instance issue the following command:

```
$ rake_refresh
``` 

Take a deep breath. Enjoy fast rake command completion.
