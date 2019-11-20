---
layout: post
title: "Squish Those Strings"
author: jasonschweier
date: 2017-04-20T14:19:56+00:00
---

While reading some Rails code, I came across a deprecation warning:

```ruby
ActiveSupport::Deprecation.warn(<<-MESSAGE.squish)
  `redirect_to :back` is deprecated and will be removed from Rails 5.1.
  Please use `redirect_back(fallback_location: fallback_location)` where
  `fallback_location` represents the location to use if the request has
  no HTTP referer information.
MESSAGE
```

What caught my eye was the `squish` method on the heredoc. It's common to see methods after heredocs to clean up formatting, but `squish` is a great method name.

`squish` removes all leading and trailing whitespace, then replaces all consecutive whitespace with a single space. One application has been cleaning up long string messages that use the line continuation operator. The [community style guide](https://github.com/bbatsov/ruby-style-guide) says to only use line continuations for concatenating strings, but I think `squish` is cleaner:

```ruby
long_string = "a long string " \
              "spanning " \
              "three lines"
# => "a long string spanning three lines"

better_long_string = "a long string
                      squished to a single line
                      without extra spaces or backslashes".squish
# => "a long string squished to a single line without extra spaces or backslashes"
```

An all-too-common caveat: `squish` is an extenstion method from `active_support`.
