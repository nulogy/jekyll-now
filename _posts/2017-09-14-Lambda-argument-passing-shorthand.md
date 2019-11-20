---
layout: post
title: "Lambda argument passing shorthand"
author: evanbrodie
date: 2017-09-14T18:40:15+00:00
---

Suppose that I have a Ruby lambda like so:

```ruby
greeting = -> name { "Hello #{name}" }
```

The conventional way of calling this lambda is like so:

```ruby
greeting.call("Ned") # "Hello Ned"
```

However, for those of you dreading having to type in `call` (hello, JavaScript developers), you can use this syntactic sugar instead:

```ruby
greeting["Ned"]
greeting.("Ned")
```

**Source:** https://stackoverflow.com/questions/18774139/how-works-with-lambdas

# UPDATE

I am now a sad panda to learn that this shorthand syntax is not recommended in the *ruby-style-guide*: https://github.com/bbatsov/ruby-style-guide/issues/205 https://github.com/bbatsov/ruby-style-guide/blob/master/README.md#proc-call

It's still a cool learning for me to know that this syntax exists in the first place, though.
