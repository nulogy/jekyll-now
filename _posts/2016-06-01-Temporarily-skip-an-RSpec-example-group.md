---
layout: post
title: "Temporarily skip an RSpec example group"
author: alistairmckinnell
date: 2016-06-01T03:31:57+00:00
---

I knew about prefixing an RSpec example with `x` to skip it. I just found out that a `describe` or `context` example group can also be [temporarily skipped](https://relishapp.com/rspec/rspec-core/v/3-4/docs/pending-and-skipped-examples/skip-examples) using `xdescribe` and `xcontext`.

How did I find out? [RTSL](https://blog.codinghorror.com/learn-to-read-the-source-luke/)

Special bonus: the focus effect works similarly: `fit`, `fdescribe`, and `fcontext`.
