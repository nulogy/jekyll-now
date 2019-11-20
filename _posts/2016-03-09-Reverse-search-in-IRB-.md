---
layout: post
title: "Reverse-search in IRB."
author: ryandevilla
date: 2016-03-09T17:08:38+00:00
---

You can reverse-search through previously entered statements in IRB by pressing Ctrl-R:

```ruby
~
❯ irb
2.1.6 :001 ❯ def something_complicated(x,y); x + y; end
 =❯ :something_complicated
2.1.6 :002 ❯ quit

~ 10s
❯ irb
(reverse-i-search)`compli': def something_complicated(x,y); x + y; end
```

Happy hacking!
