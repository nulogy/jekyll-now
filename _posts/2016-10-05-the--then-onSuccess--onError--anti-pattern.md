---
layout: post
title: "the .then(onSuccess, onError) anti-pattern"
author: jasonkurian
date: 2016-10-05T17:50:21+00:00
---

Before:

```js
somePromise().then(
  function onSuccess (res) {
    // stuff happens, but oh no!
    // an error is thrown in here!
  },
  function onError (err) {
    // request-only error handler
  }
);
```

After:

```js
somePromise()
  .then(function onSuccess (res) {
    // stuff happens, but oh no!
    // an error is thrown in here!
  })
  .catch(function onError (err) {
    // yay! The error thrown in the function above
    // can be handled here or rethrown to be handled elsewhere.
  });
```

More details [here](http://stackoverflow.com/a/24663315/1444541).
