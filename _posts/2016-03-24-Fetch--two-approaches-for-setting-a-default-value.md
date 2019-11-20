---
layout: post
title: "Fetch: two approaches for setting a default value"
author: bryanmacdiarmid
date: 2016-03-24T00:34:38+00:00
---

When using `#fetch` to assign a default value, the default can be passed either as an argument or as a block.  

**What are the implications for choosing one approach over the other?**

```ruby
# Option 1: block
setting = settings.fetch('key') { default_setting }

#Option 2: argument
setting = settings.fetch('key', default_setting)
```

When the default value is passed as a block, it is only evaluated when needed (lazy evaluation).

The argument approach could lead to serious performance issues if the default is an expensive operation. 
