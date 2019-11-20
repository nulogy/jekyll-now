---
layout: post
title: "Move cursor word by word on iTerm"
author: robertdooley
date: 2018-02-08T22:40:26+00:00
---

Problem
===
Cursor navigation can be slow on iTerm

Solution
===
Enable word by word cursor movement

~~~
Preferences > Profiles > Keys > Select + to add new key mapping
~~~


To move left:

~~~
Keyboard Shortcut: ⌥ ←
Action: Send Escape Sequence
Esc+ b
~~~

To move right

~~~
Keyboard Shortcut: ⌥ →
Action: Send Escape Sequence
Esc+ f
~~~


[Source](https://apple.stackexchange.com/questions/154292/iterm-going-one-word-backwards-and-forwards)
