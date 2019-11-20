---
layout: post
title: "Using module_function instead of extend self"
author: jordanneville
date: 2018-01-19T14:12:10+00:00
---

It's a common pattern to use `extend self` inside ruby module to make all methods available in a static context/declared as class methods.

Instead of this, you can use `module_function` instead which will do the same as extend self but also have the added benefit of making those method private instance methods when they are included in another file.

```
module UserNameFormatter
  module_function

  def format_name(user)
    "#{user.name}"
  end
end

class User
  include UserNameFormatter

  def something
    format_name(self)
  end
end
```
