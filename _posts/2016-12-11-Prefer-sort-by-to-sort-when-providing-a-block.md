---
layout: post
title: "Prefer sort_by to sort when providing a block"
author: alistairmckinnell
date: 2016-12-11T02:19:31+00:00
---

Prefer the `sort_by` method over the `sort` method whenever you provide a block to define the comparison.

Common form:

```
line_adds.sort { |x, y| x.elements["ItemRef/ListID"].text <=> 
  y.elements["ItemRef/ListID"].text }
```

Preferred form:

```
line_adds.sort_by { |x| x.elements["ItemRef/ListID"].text }
```

For small collections both techniques have similar performance profiles. When the sort key is something simple like an integer there is no performance benefit from `sort_by`.

The performance difference is especially noticeable if the sort key is expensive to compute and/or you have a large collection to sort.

The algorithm that yields the performance benefit is known as the [Schwartzian Transform](https://en.wikipedia.org/wiki/Schwartzian_transform).
