---
layout: post
title: "Chef override attributes vs chef-client -j switch"
author: arturopie
date: 2017-04-07T16:29:12+00:00
---

When applying recipes via `chef-client`,  you can override attributes via the --json-attributes (or -j) switch. However, the `override_attributes`   option on `roles`, `environments` and  `recipes` has higher precedence over the --json-attributes switch.

For more info about Chef attribute precedence, use [this](https://docs.chef.io/attributes.html#attribute-precedence) as a reference. The attributes set via `--json-attributes` are "normal" attribute types.

