---
layout: post
title: "Jumping/deleting by matching tags"
author: clemenspark
date: 2016-03-09T19:28:17+00:00
---

Let's say you have the following:

```ruby
def a_method
  "a return value"
end
```

If you put your cursor on `def` and type `%`, it goes to `end`.

If you put your cursor on `def` and type `d%`, it deletes the entire method!
