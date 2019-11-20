---
layout: post
title: "An Improvement to the Behaviour of the Git Pager"
author: alistairmckinnell
date: 2017-05-19T11:45:09+00:00
---

First, capture your current git pager settings (in case you want to go back):

````
git config --list | grep core.pager
````

Second, configure your new and improved git pager settings:

````
git config --global core.pager "less $LESS --tabs=2 -RFX"
````

````
--tabs=2: Is just right for displaying Ruby diffs

-R: Repaint the screen, discarding any buffered input
-F: Causes less to exit if a file is less than one screens worth of data
-X: Leave file contents on screen when less exits.
````

If you want to get even fancier consider [diff-so-fancy](https://github.com/so-fancy/diff-so-fancy).
