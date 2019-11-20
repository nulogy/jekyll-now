---
layout: post
title: "Safe Navigation Operator"
author: jasonschweier
date: 2018-01-29T22:30:09+00:00
---

If you have worked in a Rails project, you have probably came across the `try` and `try!` methods. `try` saves us from checking conditions before drilling-down through a message chain. `try!` is more restrictive; it raises when the receiver does not respond to the method:

```ruby
require "active_support"
require "active_support/core_ext/object/try"

User = Struct.new(:name)

users = [User.new("Jason")]

users.first.try(:name)
# "Jason"

users.first.try(:unknown_method)
# nil

users.first.try!(:unknown_method)
# NoMethodError: undefined method `unknown_method' for #<struct User name="Jason">
```

Note these methods are provided by `ActiveSupport`. As of Ruby 2.3, this behaviour is now available in the language, called the *safe navigation operator* `&.`:

```ruby
users = [User.new(name: "Jason")]
users.first&.name
# "Jason"

users = []
users.first&.name
# nil
```

## Gotchas

When an object does not respond to a method, `&.` behaves like `try!`; it raises an error. However, `nil` seems to break this pattern:

```ruby
# behaviour like try!
user&.unknown_method
# NoMethodError: undefined method `unknown_method' for #<struct User name="Jason">

# given that
nil.nil?
# true

# this is confusing
nil&.nil?
# nil
```

The last example has a simple explanation: `&.` checks the receiver. Since the receiver is `nil`, `&.` immediately returns `nil`. It does not matter that `nil` responds to the message.
