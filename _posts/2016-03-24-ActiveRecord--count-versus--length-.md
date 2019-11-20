---
layout: post
title: "ActiveRecord #count versus #length "
author: evanbrodie
date: 2016-03-24T14:53:30+00:00
---

Let's say you have an ActiveRecord model with a `has_many` association. Ever wonder why you receive different results from `#count` and `#length` after you append to that has_many collection? Consider this rough example where `Parent` and `Kid` are ActiveRecords and `Parent` will `has_many :kids`:

```ruby
parent = Parent.create!
parent.kids.create! name: 'Evan'
puts "Current length is #{parent.kids.length}"
puts "Current count is #{parent.kids.count}"
```

The output will be:

```
Current length is 0
Current count is 1
```

The difference in results appear to be happening because of how `length()` and `count()` compute their results. `length()` is only considering what is loaded into heap memory ("cached"), while `count()` will actually check what is loaded into the DB.

Here's a [great blog post](http://mensfeld.pl/2014/09/activerecord-count-vs-length-vs-size-and-what-will-happen-if-you-use-it-the-way-you-shouldnt/) about the difference between the two methods, as well as `size()`.
