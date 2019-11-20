---
layout: post
title: "Inheritance does not affect method visibility"
author: ryandevilla
date: 2016-03-24T17:49:19+00:00
---

Contrary to visibility conventions in other languages such as Java, Ruby methods defined under a ``private``
block in a class definition are still accessible by that class' children:

```rb
class Foo
  private

  def private_method!
    p "Hello world!"
  end
end

class Bar < Foo
  def uses_private_method
    private_method!
  end
end

b = Bar.new
b.uses_private_method # => "Hello world!"
```

This is because the ``private`` keyword in Ruby has nothing to do with inheritance;
declaring a method as ``private`` only adds the restriction that it may not be invoked
with an explicit receiver, as illustrated below:

```rb
class Quux < Foo
  def explicit_receiver
    self.private_method!
  end

  def implicit_receiver
    private_method!
  end
end

q = Quux.new
q.explicit_receiver # => NoMethodError: private method `private_method!' called for #<Quux:0x007fee689e0ff8>
q.implicit_receiver # => "Hello world!"
```
