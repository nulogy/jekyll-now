---
layout: post
title: "Testing an Independent Mixin With RSpec"
author: alistairmckinnell
date: 2016-08-22T17:19:45+00:00
---

Objective: write a spec for the `Inventory::Query` mixin.

Note: the mixin is independent of the including class as it does not depend on any instance variables or instance methods.

**Original Approach**

```
class InventoryQueryTest
  include Inventory::Query
end
```

```
subject(:inventory_query) { InventoryQueryTest.new }
```

**Preferred Approach**

```
subject(:inventory_query) { (Class.new { include Inventory::Query }).new }
```

**Advantage**

Simpler and avoids polluting the global namespace with a test class.

