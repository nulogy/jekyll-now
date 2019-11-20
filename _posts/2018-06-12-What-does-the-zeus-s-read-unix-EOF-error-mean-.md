---
layout: post
title: "What does the zeus's read unix EOF error mean?"
author: clemenspark
date: 2018-06-12T21:47:34+00:00
---

Question
====

I'm running [zeus](https://github.com/burke/zeus), and it dies with the following error:

```
slavenode.go:226: [boot] read unix ->: EOF
```

What on Earth could be causing that?
How do I fix it?

Answer
====

UPDATE (2018-06-13): I realized that this is one possible fix to this issue. Still useful info, so I'll leave it here.

Run `bundle install`

Source: https://github.com/burke/zeus/issues/641

