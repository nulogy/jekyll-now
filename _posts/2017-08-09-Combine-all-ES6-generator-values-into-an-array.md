---
layout: post
title: "Combine all ES6 generator values into an array"
author: evanbrodie
date: 2017-08-09T23:12:40+00:00
---

The [ES6 spread operator](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Operators/Spread_operator) can be applied to an *iterable* to combine all its results into one single array. A trivial use case for this is to merge extra elements into an existing array (ie, `[...existingArray, 2, 3]`).

This usage of the spread can be applied to a [Generator](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Statements/function*) to combine all the results of the calls to `next()` into one array. This serves as syntactic sugar to replace needing to use a *for-of loop* to do the same operation. Here's an example (illustrative purposes only, ignore that this is not the best way to solve this problem):

```javascript
function* evenNumbersGenerator(maxNum) {
  for (let i = 0; i <= maxNum; i += 1) {
    if (i % 2 == 0) {
      yield i;
    }
  }
}

...

const evenNumbersTo100 = [...evenNumbersGenerator(100)];
```

**Side Learning:** Generator functions cannot be declared as an *arrow function*, because they have to be declared as a "non-method function".
