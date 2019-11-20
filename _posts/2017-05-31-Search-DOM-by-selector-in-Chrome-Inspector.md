---
layout: post
title: "Search DOM by selector in Chrome Inspector"
author: evanbrodie
date: 2017-05-31T17:32:18+00:00
---

## Problem

I want to select a DOM element by CSS selector on my React-generated web page for debugging purposes. In this case, I am trying to test out CSS selectors to be used in my Capybara acceptance test.

## Solution

~~Use jQuery~~ NO, DON'T DO THAT!

A neat feature of the Chrome Web Inspector is that I can search an entire page by CSS Selector, without needing to litter my code with `debugger` statements. Just open up the Elements tab and then press `CMD-F` (on Mac) to open up a search bar. I can now type whatever CSS Selector that I want and view the results that match. I can quickly test different selectors out, so that I can verify that I am writing my Capybara test accurately.

[Source](https://developers.google.com/web/updates/2015/05/search-dom-tree-by-css-selector)
