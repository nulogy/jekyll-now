---
layout: post
title: "Dig-ging into Data"
author: jasonschweier
date: 2018-06-27T20:59:35+00:00
---

Ruby 2.3 added a couple of `dig` methods to aid in accessing nested data.

Here's some [Hash](https://ruby-doc.org/core-2.3.0/Hash.html#method-i-dig) and [Array](https://ruby-doc.org/core-2.3.0/Array.html#method-i-dig) examples:

```ruby
hash = {
  animals: {
    furry: ["dog", "cat"],
    spikey: ["porcupine", "echidna"]
  }
}

hash.dig(:animals, :furry)
# => ["dog", "cat"]

# safely returns `nil` for missing keys
hash.dig(:plants, :yellow)
# => nil

array = [1, [[2, 3], 4, 5], 6]

array.dig(1, 0, 1)
# => 3

# dig on arrays take indexes, and repeatly call dig on the result
# thus, you have to be careful if the return type is not an array!
array.dig(2)
# => 6

array.dig(2, 3)
# => TypeError: Fixnum does not have #dig method

# and duck typing means they can be combined!
hash.dig(:animals, :spikey, 1)
# => "echidna"
```
