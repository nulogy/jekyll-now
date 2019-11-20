---
layout: post
title: "ES2015 Arrow fns do not have the arguments object"
author: jasonkurian
date: 2016-09-29T19:03:19+00:00
---

```js
const myFn = (/*unknown arity*/) => {
  console.log(arguments); //EMPTY ARRAY!
};
```

```js
function myFn(/*unknown arity*/) {
  console.log(arguments); //returns what you expect!
}
```

My takeaway: only use [arrow functions when they're necessary](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/Arrow_functions), which actually isn't that often! Plain old named JS functions are still powerful and if necessary can still easily be bound with `.bind(this)`.

Related reading: https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Functions/arguments

