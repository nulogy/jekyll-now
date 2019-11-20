---
layout: post
title: "Decorator Pattern in Ruby with SimpleDelegator"
author: shahriyarnasir
date: 2017-01-24T05:01:13+00:00
---

The [*Decorator Pattern*](https://en.wikipedia.org/wiki/Decorator_pattern) allows us to chain new behaviours to objects without modifying the underlying objects. It is an application of the [Open/Closed Principle](https://en.wikipedia.org/wiki/Open/closed_principle). This pattern is useful for example when we need to tack on logging, monitoring, and other non-functional requirements to objects.

In Java or C# this can be achieved using interfaces. In Ruby, we can use the `SimpleDelegator` class to achieve this:

```
require "delegate"

class FooDecorator < SimpleDelegator
  def bar
    "This is a decorated #{__getobj__.bar}"
  end
end

class Foo
  def bar
    "bar"
  end

  def fiz
    "Fiz"
  end
end

decorated = FooDecorator.new(Foo.new)
puts decorated.bar # outputs "This is a decorated bar"
puts decorated.fiz # outputs "Fiz"

double_decorated = FooDecorator.new(FooDecorator.new(Foo.new))
puts double_decorated.bar # outputs "This is a decorated This is a decorated bar"
```

Sources:

- http://howwedoapps.com/2014/10/03/simple-decorator-pattern-implementation-in-rails
- http://devblog.orgsync.com/2013/03/22/decorate-your-ruby-objects-like-a-boss/
