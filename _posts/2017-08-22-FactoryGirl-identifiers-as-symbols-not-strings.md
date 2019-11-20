---
layout: post
title: "FactoryGirl identifiers as symbols not strings"
author: jasonkurian
date: 2017-08-22T02:17:32+00:00
---

Why is `FactoryGirl.create(:my_object)` better than `FactoryGirl.create("my_object")`?

Symbols are immutable objects that are stored by the Ruby interpreter as a numeric ID (an implementation detail, the design of Ruby is flexible for different storage mechanisms). 

Strings, on the other hand, take up a memory footprint as large as the number of characters in the string. Using symbols will thus take up less memory and potentially be faster because the same address in memory will be used.

If you have n instances of the same string in your code, Ruby will use O(n) memory to store all those strings, however, if you have n instances of the same symbol in your code, Ruby will use O(1) memory to do the same lookup.

Further reading: https://bugs.ruby-lang.org/issues/7792#note-58

> This TIL came courtesy of a discussion with [Evan](https://til-engineering.nulogy.com/author/evanbrodie) and later on [Arturo](https://til-engineering.nulogy.com/author/arturopie) about best practices in writing test code, but shared here because it's broadly applicable and the FactoryGirl example is just one use case.
