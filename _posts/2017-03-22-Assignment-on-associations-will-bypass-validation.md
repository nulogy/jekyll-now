---
layout: post
title: "Assignment on associations will bypass validation"
author: jordanneville
date: 2017-03-22T16:06:56+00:00
---

Important gotcha that assignment to has_many associations will cause an immediate save even if callback validation fails.

`u = User.last`

`u.accounts = []`

`u.save # returns false because this user cannot have blank accounts`

`u.reload.accounts # returns empty array`

The gotcha here is that save is a no-op really. As soon as `u.accounts=[]` is called, the data is saved immediately, bypassing validation.
