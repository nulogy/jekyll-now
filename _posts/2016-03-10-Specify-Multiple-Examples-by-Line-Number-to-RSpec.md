---
layout: post
title: "Specify Multiple Examples by Line Number to RSpec"
author: ryandevilla
date: 2016-03-10T21:07:46+00:00
---

I can specify multiple examples as a colon-delimited list of line numbers to RSpec:

```bash
ryandv $ rspec my_spec.rb:2:8
Run options: include {:locations=>{"./my_spec.rb"=>[2, 8]}}
..

Finished in 0.00052 seconds (files took 0.08873 seconds to load)
2 examples, 0 failures
```
