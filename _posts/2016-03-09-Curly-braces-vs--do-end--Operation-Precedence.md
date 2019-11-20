---
layout: post
title: "Curly braces vs. do/end: Operation Precedence"
author: evanbrodie
date: 2016-03-09T19:35:34+00:00
---

Choosing whether you use `{ ... }` or `do ... end` around your blocks is more than just a stylistic choice in Ruby. It also affects the way that an operation will be executed because your choice also specifies the *Operation Precedence* to use. In a nutshell, _a block curly braces has higher precedence than a block with do/end._

Consider this example from a [great Stackoverflow post](http://stackoverflow.com/a/5587399/814576):

```ruby
f param { do_something() }
```

will execute differently than

```ruby
f param do do_something() end
```

The former will bind the block to `param`, while the latter will bind the block to `f`. The more you know...
