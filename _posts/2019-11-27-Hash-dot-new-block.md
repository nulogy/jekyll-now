---
layout: post
title: "Hash.new with a block"
author: podrezo
date: 2019-11-27
excerpt: "I was recently following a great blog article on memoization in Ruby by Justin Weiss and it made perfect sense until I got to the last part which was most relevant for my purposes - \"And what about parameters?\". Here, the article uses a pattern of memoization that involves a `Hash.new` that is supplied a block. [Continued...]"
---

I was recently following a [great blog article on memoization in Ruby by Justin Weiss](https://www.justinweiss.com/articles/4-simple-memoization-patterns-in-ruby-and-one-gem/) and it made perfect sense until I got to the last part which was most relevant for my purposes - "And what about parameters?". Here, the article uses a pattern of memoization that involves a `Hash.new` that is supplied a block. According to the Ruby docs this does the following:

> If a block is specified, it will be called with the hash object and the key, and should return the default value. It is the block's responsibility to store the value in the hash if required.
– [Ruby Docs](https://docs.ruby-lang.org/en/2.0.0/Hash.html)

But what does this mean exactly? It took me longer than I care to admit to figure it out but let's start with the beginning: As expected, `Hash.new` will produce an empty hash. However, the code in the block is not some sort of initializer despite how it may appear. That is, the output of

```ruby
Hash.new do |hash, key|
  ...
end
```

will always be `{}` and the block has nothing to do with the initial value. However, where the block comes into play is when accessing a value inside the hash. The block will be called if, and only if, there is no existing value for the given key. The block will also receive a reference to the hash itself so that one can assign values to it, if required. To illustrate, suppose we have this basic Fibbonaci function:

```ruby
def fib(n)
  n <= 2 ? 1 : fib(n - 1) + fib(n - 2)
end
```

and now suppose we want to optimize it by making it cache the previous values for any given `n`. The `Hash.new { ... block ...}` pattern is perfect for this. We can do:

```ruby
def fib(n)
  @fibs ||= Hash.new do |hash, key|
    hash[key] = key <= 2 ? 1 : fib(n - 1) + fib(n - 2)
  end
  @fibs[n]
end
```

So what will happen is that the first time you call `fib`, it will instantiate a new empty hash and store it to `@fibs`, then when you actually try to access the value for `@fibs[n]` it doesn't exist (since it is empty), so the block is invoked to get the default value for `n` which is going to be passed as `key`. At this point, we can compute and return the value and as an extra step we can assign it to `hash[key]` in order to cache it for later. Note that we only do `=`, not `||=` because the block, again, is only invoked when the value doesn't already exist so a `||=` operation would always do the assign in this case and the `||` part is just doing an unnecessary comparison in that case.

To give you an idea of the processing time decrease one gets by memoizing the above `fib` function, to compute the first 35 Fibonacci numbers it took my machine 3.6 seconds without memoization and 81.221 µs (microseconds) with the memoization pattern.

Happy hashing!
