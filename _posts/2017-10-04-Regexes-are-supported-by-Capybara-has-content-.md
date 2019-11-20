---
layout: post
title: "Regexes are supported by Capybara has_content?"
author: clemenspark
date: 2017-10-04T19:42:34+00:00
---

Problem
===

I am trying to assert the presence of a button on the page by checking the button text:

`expect(page).to have_content("Close")`

Unfortunately, the page also has a dropdown that contains the option `Closed`.

Solution
===

Regex to the rescue!

`expect(page).to have_content(/Close\b/)`
