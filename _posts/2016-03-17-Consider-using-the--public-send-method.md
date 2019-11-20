---
layout: post
title: "Consider using the #public_send method"
author: alistairmckinnell
date: 2016-03-17T02:18:52+00:00
---

Prefer the #public_send method to the #send method.

```ruby
result_date = date.public_send(operation, delta)
```    
 In the example above the first parameter to the #public_send method is either "+" or "-".

