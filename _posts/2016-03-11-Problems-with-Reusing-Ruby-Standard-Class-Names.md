---
layout: post
title: "Problems with Reusing Ruby Standard Class Names"
author: evanbrodie
date: 2016-03-11T16:14:49+00:00
---

You might want to think twice before making a class that reuses the same name of a Ruby Standard Library class. If undetected, you will get strange hard-to-debug behaviour in your app. Let's explore further with this Ruby file:

```ruby
module Utils
  module String
    def self.some_useful_method
      # ...
    end
  end
end
​
module Utils
  module Foo
    def self.do_stuff(string)
      raise "Argument '#{string}' is not a string" unless string.is_a?(String)
      # ...
    end
  end
end
​
Utils::Foo.do_stuff("Hello World")
```

*Okay, so "Hello World" is a String. And a String is a String, no questions asked. Right?* Well...not quite.

```
RuntimeError: Argument 'Hello World' is not a string
```

Since `Utils::String` gets loaded by Ruby, all references to the `String` constant from code inside the `Utils` module will resolve to `Utils::String`. This example may seem simple and obvious, but imagine if these two classes were in separate files, even separate libraries. How would it feel like if you keep getting `"string".is_a? String => false` in your debugging sessions?

**MORAL OF THE STORY:** It probably isn't a good idea to reuse class names from the Ruby Standard Library. Naming the first module to `Utils::StringUtils` is likely a better idea.
