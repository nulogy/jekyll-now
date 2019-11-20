---
layout: post
title: "Block Kwargs"
author: jasonschweier
date: 2018-01-25T16:17:45+00:00
---

Ruby 2.0 introduced keyword arguments. Ruby 2.1 further added *required* keyword arguments.
It is common to see methods using kwargs:

```ruby
def some_method(keyword_arg: "Hello", required_arg:)
  puts "#{keyword_arg} #{required_arg}"
end

some_method(required_arg: "world")
# Hello world
```

However, these changes **also** apply to block arguments:

```ruby
define_method :prints_block_arguments do |default_arg: "hello", required_arg:, **others|
  puts "default_arg: #{default_arg}"
  puts "required_arg: #{required_arg}"
  
  others.each_pair do |key, value|
    puts "other arg: #{key} => #{value}"
  end
end

prints_block_arguments(required_arg: "world")
# default_arg: hello
# required_arg: world

prints_block_arguments(default_arg: "ciao", required_arg: "mondo", something: "else")
# default_arg: ciao
# required_arg: mondo
# other arg: something => else

prints_block_agruments()
# ArgumentError: missing keyword: required_arg
```
