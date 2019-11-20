---
layout: post
title: "Capybara will skip invisible elements by default"
author: jerridanquiring
date: 2017-02-24T18:52:34+00:00
---

While working on an acceptance test for a date range filter in GO, we were having an issue where Capybara couldn't find an element on the page, even though we could verify it was there. Eventually we realized that the element had an opacity of 0, and that Capybara was passing it over.
To illustrate, imagine you have an element with the id `#myElement`. 

CSS:

```css
#myElement { opacity: 0; }
```
And in your Rails spec:

```ruby
page.find("#myElement");
```

The spec will fail, because `#myElement` can't be found.

Fortunately, there is a `visible` option that can be set to `false` so that Capybara doesn't skip the element. So now, changing the line in the spec to:

```ruby
page.find("#myElement", visible: false);
```
will cause it to pass.
