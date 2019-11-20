---
layout: post
title: "Matching array subset in Ruby"
author: cameronwoloshyn
date: 2016-09-14T19:59:06+00:00
---

## Problem:
How do you evaluate whether one array is a subset of another? For example, are the elements ` [a,c]`  included in ` [a,b,c]`?

## First attempt:
I was hoping to find something like ` Array.include?([...])`, but this only checks if the array includes the argument as one of its values. 

## Second attempt:
Another approach is to pass a block into  ` Array.any?` 

```
!arr1.any? { |e| !arr2.include?(e) }
```

But the double negation is rather indirect and doesn't easily reveal the intent. 

I considered extracting a method to name the functionality:

```
def subset?(arr1, arr2)
  !arr1.any? { |e| !arr2.include?(e) }
end
```

But it's still difficult to read, as it's not clear whether `arr1`  is a subset of `arr2`, or vice versa.

## Final Solution:

The ` Enumerable` module includes a ` to_set` method to convert the array to set, and ` Set` includes a ` subset?` method.

```
arr1.to_set.subset?(arr2.to_set)
```


Technically, you need to require set.rb to get this method defined on `Enumberable`: 

```
require "set"

arr1.to_set.subset?(arr2.to_set)
```

But you get this require for free in Rails.
