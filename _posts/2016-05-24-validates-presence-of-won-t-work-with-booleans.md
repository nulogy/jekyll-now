---
layout: post
title: "validates_presence_of won't work with booleans"
author: evanbrodie
date: 2016-05-24T21:46:08+00:00
---

If you want to validate that a value for a particular boolean field exists (using ActiveRecord instead of null constraints from you DB), then you cannot use `validates_presence_of`. This is due to the way that the `blank?` works on an object with the value `false`. Instead, you will need to use this for your validation:

```ruby
 validates_inclusion_of :field_name, :in => [true, false]
```

**SEE:**

http://stackoverflow.com/questions/2883823/why-does-false-invalidate-validates-presence-of
http://apidock.com/rails/ActiveModel/Validations/ClassMethods/validates_presence_of

