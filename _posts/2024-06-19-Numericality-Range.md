---
layout: post
title: "Using a Range in a Numericality Validation"
author: alistairmckinnell
date: 2024-06-19T23:16:00
excerpt: "Rails 7.0 allows a more compact way to specify allowed values in a numericality validation."
---

Rails `7.0` allows a more compact way to specify allowed values in a numericality validation.

Instead of using combinations of `greater_than`, `greater_than_or_equal_to`, `less_than`, and `less_than_or_equal_to`, 
you can use `in` with a range.

**Before**

```ruby
  validates :setting_reuse, numericality: { greater_than_or_equal_to: 0, less_than_or_equal_to: 12 }
```

**After**

```ruby
  validates :setting_reuse, numericality: { in: 0..12 }
```

You get all the expressiveness that a range provides.
Here are more examples each showing before and after:

```ruby
  validates :setting_reuse, numericality: { greater_than_or_equal_to: 2 }
  validates :setting_reuse, numericality: { in: 2... }
```

----

```ruby
  validates :setting_reuse, numericality: { less_than: 12 }
  validates :setting_reuse, numericality: { in: ...12 }
```

