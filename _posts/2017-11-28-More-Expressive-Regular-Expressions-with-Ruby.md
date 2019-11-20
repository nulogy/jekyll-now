---
layout: post
title: "More Expressive Regular Expressions with Ruby"
author: jasonschweier
date: 2017-11-28T18:01:36+00:00
---

I came across some parsing code that contained this regular expression:

```ruby
# the first capture is the left quote
# the second capture is the string content
# the third capture is the right quote
METHOD_CAPTURE = /Module\.method\(\s*(['"])(.+?)(['"])\s*\)/
```

This regexp is matching the string contents of a particular method call. It captures three pieces of information, mentioned in the comments.

This code is not self-documenting. We have three comments explaining the captures, and a regexp we must parse in wetware.

Furthermore, numerical indexes are difficult to track and modify in complicated regexps. [PCRE](https://www.pcre.org/original/doc/html/pcrepattern.html#SEC16) supports named captures; denoted in Ruby by `(?<name>pattern)`.

To make the comments superfluous, let's refactor using the following:

1. Use named capture groups
2. Use interpolation to give descriptive names to common components
3. Don't capture needlessly (in our case, the captured quote characters are not used)
4. Prefer `[]` over escaping (personal preference)

```ruby
quote_character = %q|['"]|
optional_whitespace = "\s*"

METHOD_CAPTURE = /Module[.]method[(]#{optional_whitespace}#{quote_character}(?<string_contents>.+?)#{quote_character}#{optional_whitespace}[)]/

# #match returns an object or nil
matches = 'Module.method("some string")'.match(METHOD_CAPTURE)

# if an object, access captures by name:
matches[:string_contents] # "some string"
```

You can tailor how many named expressions/variables to use based on the complexity of the regexp.
