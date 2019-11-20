---
layout: post
title: "Default Value for Deconstructed Object Parameter"
author: evanbrodie
date: 2018-01-19T22:55:00+00:00
---

In ES6, you can deconstruct a function's object parameter to have its properties assigned to local named variables:

```js
function MyComponent({
  item: { foo, bar }
}) { ... }
```

Also in ES6, the properties of the object parameter can have a default value set:

```js
function MyComponent({
  item = "LOL"
}) { ... }
```

**TIL:** The object parameter can have *both destructuring and default values* applied to it!

```js
function MyComponent({
  item: { foo, bar } = { foo: 1, bar: 2 }
}) { ... }
```
