---
layout: post
title: "Mocha: Fail on any console error message"
author: evanbrodie
date: 2017-02-24T22:10:56+00:00
---

**PROBLEM**

I want to write a Mocha (JS) test that will fail if there is any warning printed to the console to fail. My use case to necessitate this requirement is that I want to test whether the correct prop type is passed to a React component. `PropTypes` exists for this purpose, but would only print out a message to the console instead of failing.

**SOLUTION**

Use the following code, either at the beginning of your test file or a global helper such as `specHelper.js`, to stub out the implementation of `console.error` to throw an `Error` and thus fail the test.

```js
before(() => stub(console, "error", (warning) => {
  throw new Error(warning);
}));

after(() => console.error.restore());
```

**Reference:** [this gist](https://gist.github.com/scmx/d98cc058a7c3dfef7890).
