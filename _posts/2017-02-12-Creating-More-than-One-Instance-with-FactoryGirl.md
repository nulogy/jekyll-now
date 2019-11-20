---
layout: post
title: "Creating More than One Instance with FactoryGirl"
author: alistairmckinnell
date: 2017-02-12T19:03:18+00:00
---

In some [test fixtures](http://en.wikipedia.org/wiki/Test_fixture#Software) I need to create an array of instances . [FactoryGirl](https://github.com/thoughtbot/factory_girl) provides the `create_list` method for exactly this purpose. 

To create four shipments on an outbound trailer: 

```ruby
FactoryGirl.create_list(:shipment, 4, outbound_trailer: trailer)
```

In the example above, `create_list` returns an array containing the newly created shipments.
