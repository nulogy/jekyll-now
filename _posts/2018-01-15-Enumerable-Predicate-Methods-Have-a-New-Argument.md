---
layout: post
title: "Enumerable Predicate Methods Have a New Argument"
author: jasonschweier
date: 2018-01-15T14:44:26+00:00
---

`Enumerable#grep` accepts an argument that returns elements that are `true` using *case equality* (`===`). These elements can then be passed to its block for further proccessing:

```ruby
fruits = %w(apples orange grapes)
fruits.grep(/s$/) # => ["apples", "grapes"]
fruits.grep(/s$/) { |e| e.start_with?("a") } # => [true, false]
```

In Ruby 2.5, this [parameter argument](https://bugs.ruby-lang.org/issues/11286) was added to the `Enumerable` predicate methods `all?`, `none?`, `one?`, and `any?`.

```ruby
fruits = %w(apples orange grapes)
fruit.any?(/s$/) # => true

# === works with more than Regexes!
[1, 3.14, 2ri].all?(Numeric) # => true
[0, 1, 2, 3].all?(1..10) # => false
[0, 5].one?(1..3) # => false
[0, 5].none?(1..3) # => true
```
