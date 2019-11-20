---
layout: post
title: "Serializing many value objects to database columns"
author: diogobiazus
date: 2017-02-02T15:10:56+00:00
---

While reading the IDDD book on serialization of value objects there is this description of an approach called "ORM and Many Values Serialized into a Single Column". It's good to note that some of the main objections to this approach are technology related and barely applicable in a world of Rails' ActiveRecord + PostgreSQL.

The objections presented by the book are:

* Column width: It mentions that serializing to varchar fields will meet some limitations imposed by Oracle and MySQL implementations. In PostgreSQL, besides having composite types (e.g. json or array), the limit on any column is much higher [(1GB)](https://www.postgresql.org/about/).
* Must query: The book states that if the values must be queried this approach cannot be used. This is another limitation imposed by the underlying technology. Using PostgreSQL one can easily query composite values and even created indexes over them.
* Requires custom user type: This is not related to the database technology but is heavily biased towards hibernate. In Rails' ActiveRecord the custom serializers require very little boilerplate and it offers out of the box support for [json, array and range types](http://edgeguides.rubyonrails.org/active_record_postgresql.html).
