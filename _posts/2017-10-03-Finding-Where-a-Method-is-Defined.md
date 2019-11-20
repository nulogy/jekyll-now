---
layout: post
title: "Finding Where a Method is Defined"
author: alistairmckinnell
date: 2017-10-03T02:27:36+00:00
---

One great thing about Ruby is how flexible it is. Although sometimes it can be hard to determine where a method definition comes from. 

One useful technique to pull out in just this circumstance is the `source_location` method.

For example, suppose you see a call to the `quantity` method in a spec and you wonder where its definition comes from.
Do some [puts debugging](https://tenderlovemaking.com/2016/02/05/i-am-a-puts-debuggerer.html) by adding this line:

```ruby
puts method(:quantity).source_location
```

