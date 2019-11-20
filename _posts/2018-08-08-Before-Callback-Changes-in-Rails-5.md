---
layout: post
title: "Before Callback Changes in Rails 5"
author: jasonschweier
date: 2018-08-08T20:22:21+00:00
---

In Rails 4 and below, callbacks like `before_validation` always had a gotcha that you had to watch out for:

```ruby
before_validation :ensure_field_is_false_when_condition

def ensure_field_is_false_when_condition
  self.field = false if condition?
end
```

When `condition?` is `true`, the assignment happens. However, assignment returns the value that _was_ assigned, so the `before_validation` receives the returned value `false`. [As the docs mention](https://api.rubyonrails.org/v4.2.10/classes/ActiveRecord/Callbacks.html):

> If the returning value of a before_validation callback can be evaluated to false, the process will be aborted and Base#save will return false.

This is usually handled by an explicit `return` (*i.e.* `nil` does not stop the callback chain):

```ruby
def ensure_field_is_false_when_condition
  self.field = false if condition?
  
  # extraneous return that is not Ruby-ish
  return
end
```

# Rails 5 Update

There is a great change to the `before_validation` [callback behaviour in Rails 5](https://api.rubyonrails.org/classes/ActiveRecord/Callbacks.html):

> If the before_validation callback throws :abort, the process will be aborted and ActiveRecord::Base#save will return false.

This makes halting the callback chain much more transparent and intention revealing:

```ruby
before_validation :safely_assign_false, :always_halt_validation

def safely_assign_false
  self.field = false
end

def always_halt_validation
  throw(:abort)
end
```
