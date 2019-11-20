---
layout: post
title: "Ruby print to replace contents on same line"
author: evanbrodie
date: 2016-11-23T22:06:59+00:00
---

In Ruby, the `print` command can be used with the `'\r'` (carriage return) character to bring the cursor back to the beginning of the printed line, so that the next `print` call will replace the contents already outputted to that line. This is a very useful tool for printing status updates in a CLI script. For example:

```ruby
print "#{index} done. Progress: %.2f%" % (index.to_f / items * 100).round(2) + "\r" if (index % 10) == 0
```

This will print and replace a line in STDOUT to report the status of a list of items being processed by a function, like so:

> 200 done. Progress: 15%

Typewriters still hold a lasting impact on modern-day computing!
