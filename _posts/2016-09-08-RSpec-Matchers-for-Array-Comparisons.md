---
layout: post
title: "RSpec Matchers for Array Comparisons"
author: alistairmckinnell
date: 2016-09-08T10:47:05+00:00
---

Whenever you are matching arrays ask yourself two questions:

* Is order important?
* Am I matching a subset of the elements or all of the elements?

How I decide on a matcher:

1. Choose between the `eq` and `be` matcher if order is important.
2. Choose the `include` matcher if you want to match on a subset of the elements.
3. Choose between the `match_array` and `contain_exactly` matcher if you want to match all elements (and order doesn't matter).

Below is an example of an improvement to a previously intermittent test. I replaced the `eq` matcher with the `match_array`  matcher because I wanted to match all `location_ids` and order doesn't matter.

```
expect(location_ids).to eq([location_2.id, location_3.id])
```

```
expect(location_ids).to match_array([location_2.id, location_3.id])
```

The root cause of the intermittent test was that the locations were being retrieved from the database with no order specified. From the PostreSQL documentation: *If sorting is not chosen, the rows will be returned in an unspecified order. The actual order in that case will depend on the scan and join plan types and the order on disk, but it must not be relied on.*

