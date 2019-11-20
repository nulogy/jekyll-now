---
layout: post
title: "Retrieving the IDs for a Model"
author: alistairmckinnell
date: 2016-08-25T06:37:05+00:00
---

Prefer the `ids`  method to  `map(&:id)` when you want to retrieve an array of model IDs.

**Example**

```
receipt.receive_orders.ids
```

```
receipt.receive_orders.map(&:id)
```
In the example above, using `ids` avoids fetching the receive orders from the database.

**Rails Source**

```
def ids
  pluck primary_key
end
```
