---
layout: post
title: "Apollo flattens your GraphQL data!"
author: devanhurst
date: 2019-09-06T20:07:28+00:00
---

Suppose we're retrieving items in an eCommerce cart:

```
query {
  cartItems() {
    item {
      product {
        id
        size
      }
    }
  }
}
```

Data is returned as expected.

```
{
  cart_items: {
    0: {
      product: {
        id: "nulogy-shirt",
        size: "medium",
      },
    },
    1: {
      product: {
        id: "nulogy-shirt",
        size: "large",
      },
    },
  }
}
```

In our cart, we have two `nulogy-shirt` items. One is medium, one is large, so they're not quite the same product. When this data hits Apollo, however…

```
{
  cartItems: {
    0: {
      product: {
        id: "nulogy-shirt",
        size: "medium",
      },
    },
    1: {
      product: {
        id: "nulogy-shirt",
        size: "medium",
      },
    },
  }
}
```

All the data is stored in Apollo’s cache as a flattened array. Regardless of how they’ve been nested inside other objects, no two objects of the same type can share an ID. Otherwise, the first object overwrites all others.

Apollo makes this comparison based on the `id` or `_id` field (or a user override). If not found, the object’s keys become dependent on the nesting (`ROOT_QUERY.cartItems.0.product` and `ROOT_QUERY.cartItems.1.product`)

If you experience this, a good solution is to rename the ID field for the query's response.

See https://www.apollographql.com/docs/react/advanced/caching/#normalization
