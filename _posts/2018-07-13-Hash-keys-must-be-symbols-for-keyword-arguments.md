---
layout: post
title: "Hash keys must be symbols for keyword arguments"
author: jiyou
date: 2018-07-13T14:49:45+00:00
---

Recently our team worked on a ticket which required us to remove the tooltips for Edit, Delete button. 

As an initial approach, we changed the signature by parameterizing the tooltip, and inserted into #link_to helper. To preserve the options parameter, we converted it into a keyword argument (**options).

```ruby
def link_to_delete_remote(object, path, tooltip: _("Delete"), **options)
   …
   link_to(options[:title], path, options.merge('data-bad-after': js, id: link_id, title: tooltip, remote: true))
end
``` 
```ruby
 <%= link_to_delete_object(job, tooltip: nil) %>
```

 However, bunch of specs started failing with the following message.

```ruby
# ArgumentError: wrong number of arguments (given 3, expected 2)
```

Turns out, there were few callers of the method who were passing in an object that contains String keys, and they weren’t being used as keyword arguments…

```ruby
<%= link_to_delete_object(
      attachment,
      "some-string-key" => _("some_string_value"),
      "another-string-key" => true
    ) %>
```

In the end, we reverted the signature, injected `tooltip: nil` to `options` object, and just inlined `options.fetch(:tooltip, _(“Delete”))`

```ruby
  def link_to_delete_remote(object, path, options = {})
    ...
    link_to(options[:title], path, options.merge('data-bad-after': js, id: link_id, title: options.fetch(:tooltip, _("Delete")), remote: true))
  end

```
