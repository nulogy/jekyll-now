---
layout: post
title: "Exclusion using File Masks"
author: joneriksuero
date: 2017-06-20T15:05:18+00:00
---

When using **"Find in Path.."** functionality to find a word across multiple files, **file masks** can be used to match certain types of files. For example, using \*.rb will only look through Ruby files. On the other hand, if you want to exclude Ruby files instead, you can add an ! at the front (i.e. !\*.rb).

Here are other useful examples/combinations:

**all files excluding spec tests:** !\*spec.rb

**all Ruby files excluding spec tests:** \*.rb,!\*spec.rb
