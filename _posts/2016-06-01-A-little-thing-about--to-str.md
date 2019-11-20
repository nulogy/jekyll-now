---
layout: post
title: "A little thing about .to_str"
author: ryanmagowan
date: 2016-06-01T18:17:52+00:00
---

Playing with Ruby's === today and found some knowledge that's share-worthy.  I noticed in ruby docs for "string ===" a reference to ".to_str" and decided to investigate.

Nothing too exciting here, but its an important point of reference.

```
> hello = "hello"
> goodbye = "goodbye"
    
> hello === hello     #=> true
> hello === goodbye   #=> false
```

This is also what would usually be expected.  Hang in there...

```
> string = "string"
> object = Object.new
> string + object     #=> TypeError no implicit conversion
```

Here's where things get *funky*.

```
class SomeObjectWithToStr
  def to_str
    "is now a string"
  end
end

> string = "string"
> object = SomeObjectWithToStr.new

> string + object     #=> "string is now a string"
> "string is now a string" === "string" + object      #=> true
```

Hunh?  Why did that work?

<b>TIL that .to\_str is the default method call when operators force a conversion to a string.  You'll likely have to define it yourself.  Also note that the object type on the left is what the object type on the right will try to convert into.</b>

Do you know of any Objects that come with pre-defined .to\_str methods?
