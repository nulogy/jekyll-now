---
layout: post
title: "Replacing num.times.map with Array.new(num)"
author: evanbrodie
date: 2017-03-13T21:52:26+00:00
---

## Problem

I want to create an array containing objects created with an incrementing integer index parameter. For example, an array of hashes containing strings built off of the incrementing number.

## Standard Solution

```ruby
my_array = num.times.map do |index|
  build_hash(index)
end
```

BUT...rubocop didn't like this:

> ... C: Performance/TimesMap: Use Array.new with a block instead of .times.map

## Improved Solution

The improved solution allows us to build the same array with less chained methods, thus improving readability:

```ruby
my_array = Array.new(num) do |index|
  build_hash(index)
end
```
