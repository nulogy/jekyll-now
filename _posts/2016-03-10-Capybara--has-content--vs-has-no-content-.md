---
layout: post
title: "Capybara !has_content? vs has_no_content?"
author: clemenspark
date: 2016-03-10T21:08:30+00:00
---

Let's say you're using RSpec and Capybara.

What's the difference between the following:

```
  expect(page).to_not have_content("not on page")
```

and

```
  expect(page).to have_no_content("not on page")
```

Assuming that the content "not on page" is expected to disappear from the page:

The first one will wait until the Capybara default wait time is over (2 seconds), then pass the assertion.
The second one will pass as soon as "not on page" disappears from the page.

The reason the first one waits is because has_content? waits for the content to appear.  When the timeout expires, it returns false, which passes the to_not assertion.

Never use `to_not have_content` or `!has_content` in Capybara.
