---
layout: post
title: "Reading Text File with Byte Order Mark Using Ruby"
author: shahriyarnasir
date: 2016-11-08T18:51:12+00:00
---

Ruby's `File.read()` can natively read a text file containing a [byte order mark](https://en.wikipedia.org/wiki/Byte_order_mark) and strip it out:

```
text_without_bom = File.read("file.txt", encoding: "bom|utf-8")
```
