---
layout: post
title: "Compounding expectations in Rspec and Chai"
author: evanbrodie
date: 2016-10-05T17:17:39+00:00
---

When I had multiple expectations on the same object in **rspec**, I would write the code like so:

```ruby
expect(page).to have_content("Foo")
expect(page).to have_content("Bar")
expect(page).to have_content("Other Stuff")
```

You can save yourself some typing if you instead use [compound expectations](https://www.relishapp.com/rspec/rspec-expectations/v/3-5/docs/compound-expectations), which is basically the usage of the `and` function after the previous expectation. Doing so will allow the previous code to be writted as such:

```ruby
expect(page).to have_content("Foo")
  .and have_content("Bar")
  .and have_content("Other Stuff")
```

The same concept also exists in the **Chai** JavaScript testing library ([documentation](http://chaijs.com/api/bdd/)):

```javascript
expect(page).to.contain("Foo")
  .and.contain("Bar")
  .and.contain("Other Stuff");
```
