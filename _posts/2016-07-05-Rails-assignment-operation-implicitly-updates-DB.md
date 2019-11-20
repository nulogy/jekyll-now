---
layout: post
title: "Rails assignment operation implicitly updates DB"
author: jordanneville
date: 2016-07-05T17:40:01+00:00
---

In Rails, you may fall into a trap where simply assigning a value to an ActiveRecord object's properties may cause a DB write immediately.

This will occur implicitly without calling`object.save()`!

What's vulnerable?
It appears that ActiveRecord objects that expose a property via association are vulnerable to this quirk. This *won't* happen for properties that have no association.

For example, given the following:

`class MyClass < ActiveRecord::Base`

`  has_many :children`

`  attr_accessor :property_name`

`end`

....


`obj = MyClass.find(1)`

`obj.children = [child_one,  child_two,  child_three] <=== this will write to the DB immediately!`

`obj.property_name = 'value' <=== this is in memory only, the DB has not been updated`

`obj.save <=== property_name is updated in the DB now`

This may cause issues if your save implies validations and the validations fail. In this case, the associated property was updated in the DB but the other properties were not because of the validation failure.

Yikes!
