---
layout: post
title: "Show definition of a method at runtime in Ruby"
author: arturopie
date: 2016-04-02T18:37:01+00:00
---

Many people know about `method(:foo).source_location` to find where a method is defined at runtime. I just found a better way by using [pry](http://pryrepl.org/).

From the pry console, run: 

```
[8] pry(main)> show-source Bar.scoped.where
From: /Users/arturo/.rvm/gems/ruby-2.2.6/gems/activerecord-3.2.22.1/lib/active_record/relation/query_methods.rb @ line 132:
Owner: ActiveRecord::QueryMethods
Visibility: public
Number of lines: 7

def where(opts, *rest)
  return self if opts.blank?

  relation = clone
  relation.where_values += build_where(opts, rest)
  relation
end
```

Happy Hacking!
