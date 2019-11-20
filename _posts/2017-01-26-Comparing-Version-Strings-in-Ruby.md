---
layout: post
title: "Comparing Version Strings in Ruby"
author: jasonschweier
date: 2017-01-26T02:14:56+00:00
---

While writing a Ruby script, I needed to check the the version of a binary dependancy. The `--version` switch gets me the data, but how to compare to the required version?

The binary follows [semver](http://semver.org/), so a quick and dirty attempt might be:

```ruby
"1.4.2".gsub(".", "") >= "1.3.1".gsub(".", "")
# => true
```

Unfortunately, this is misleading: we are lexicographically comparing the strings and these strings happen to have the same length. Thus, `"142"` comes after `"131"`.

Testing that version `"1.200.0"` is newer than `"1.9.0"` will fail as `"120"` comes before `"190"`.

It would be straight-forward to write a small class to parse the string and compare the major, minor, and patch values. But, Ruby has a quick solution provided by RubyGems. Since Ruby 1.9, RubyGems has been included in Ruby's standard library:

```ruby
Gem::Version.new("1.200.1") >= Gem::Version.new("1.3.1")
# => true
```

`Gem` also provides a way handle pessimistic constraints:

```ruby
dependency = Gem::Dependency.new("", "~> 1.3.1")
dependency.match?("", "1.3.9")
# => true
dependency.match?("", "1.4.1")
# => false
```
