---
layout: post
title: "Debug Arrow Functions With Comma Operator"
author: evanbrodie
date: 2018-01-19T22:48:43+00:00
---

Use the [Comma Operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comma_Operator) to execute many JavaScript expressions in one 'location', but only return the value from the last expression.

This is commonly used in classic `for` loops, but has an interesting use case to quickly debug a single-line arrow function. For example, suppose you wanted to throw a `console.log()` into this function:

```js
const myFunc = value => doCrazyOperation(value.foo);
```

Without the comma operator, this function would have to be expanded into a multi-line "block" function with a `return` statement, which is relatively quite longer:

```js
const myFunc = (value) {
  console.log("value", value);
  return doCrazyOperation(value.foo);
};
```

With the *Comma Operator*, this debugging is much easier to write and maintain:

```js
const myFunc = value => (console.log("value", value), doCrazyOperation(value.foo));
```
