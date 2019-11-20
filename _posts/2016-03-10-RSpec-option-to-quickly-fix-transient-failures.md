---
layout: post
title: "RSpec option to quickly fix transient failures"
author: arturopie
date: 2016-03-10T04:24:44+00:00
---

## Problem:
How do I quickly find the smallest set of tests to reproduce a transient RSpec failure?

## Context:

Sometimes, we find non-deterministic RSpec failures in our test suite that we often call transient failures. These tests only fail when they are run in a specific order (aka, using the same RSpec order seed), and they always pass when run in isolation. 

## Solution:

RSpec provides an option to find the minimum number of tests to run to reproduce the failure by doing bisection.

To use it, run RSpec with the order seed of one of the fail runs, and the --bisect option. For example,

```
rspec spec/cool_feature_spec.rb --seed 21952 --bisect
```

and RSpec will find the minimum reproduction command.

```
....
The minimal reproduction command is:
  rspec './spec/cool_feature_spec.rb[1:1:1,1:1:2]' --seed 21952
```
