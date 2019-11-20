---
layout: post
title: "Database Column \"type\" is reserved in Rails"
author: ryanmagowan
date: 2016-05-20T21:40:56+00:00
---

I made a database column called "type".  It contained a string.  It was bound to Object.  Everything was cool.

I wanted to create my object. But I kept getting this error.

```
object = Object.create(food: "P&L Burger", name: "The Matty", type: "Burgers")

**************************************
Invalid single-table inheritance type: 1 is not a subclass of Object
```

<b>TIL that Rails has some reserved keywords for database column names.  It just so happens that the column name "type" is reserved.  There are also other reserved column names.</b>

See: <a href="http://edgeguides.rubyonrails.org/active_record_basics.html#schema-conventions">Active Record Basics: 2.2 Schema Conventions</a>

The "type" column is reserved for single-table-inheritance where the Ruby Object name would be stored in the "type" column and would be accessible through object.type #=> Object

See: <a href="http://api.rubyonrails.org/classes/ActiveRecord/Base.html#class-ActiveRecord::Base-label-Single+table+inheritance">Single Table Inheritance</a>
