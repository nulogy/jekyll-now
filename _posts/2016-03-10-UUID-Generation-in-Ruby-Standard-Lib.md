---
layout: post
title: "UUID Generation in Ruby Standard Lib"
author: seankirby
date: 2016-03-10T02:39:45+00:00
---

No need for fancy gems in order to generate [RFC4122](https://www.ietf.org/rfc/rfc4122.txt) Version 4 compliant UUID strings. 

```ruby
>> require 'securerandom'
=> true
>> SecureRandom.uuid
=> "af04813c-6d80-4277-b4e7-7193f7413876"
```
