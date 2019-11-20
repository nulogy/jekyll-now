---
layout: post
title: "Def keyword can also be used as a begin statement"
author: evanbrodie
date: 2018-02-01T19:21:11+00:00
---

In Ruby, the `begin` keyword for exception handling (ie, `begin...rescue...ensure`, traditionally `try...catch...finally` in other languages) is optional. You can have a method that only declares a `rescue` or an `ensure` statement without `begin`. That's because the `def` statement in the method can serve the same purpose as `begin`. This means that this method:

```ruby
def edit
  begin
    @user = find(params[:id])
    ...
  rescue ActiveRecord::RecordNotFound
    redirect_to :back
  end
end
```

Can legally be shortened to:

```ruby
def edit
  @user = find(params[:id])
  ...
rescue ActiveRecord::RecordNotFound
  redirect_to :back
end
```
