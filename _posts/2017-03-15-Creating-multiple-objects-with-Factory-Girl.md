---
layout: post
title: "Creating multiple objects with Factory Girl"
author: jordanneville
date: 2017-03-15T21:00:47+00:00
---

If you need to create more than one object from a factory, you can use the `create_list` method to accomplish this.

`
FactoryGirl.create_list(:user, 10, :supervisor)
`

Will create 10 supervisor users with the supervisor trait.
