---
layout: post
title: "Prettify JSON in the browser console"
author: clemenspark
date: 2016-08-10T13:40:10+00:00
---

Problem
===

I want to check the shape of data for an XHR request in Chrome.
So I go to the Network panel in the inspector.

When I check the response tab, I see the following:

```
[{"id":43,"child_node":{"active":true,"name":"name","created_at":"2015-05-25T16:55:09.600-04:00"},"notes":null}]
```

Not very inspectable.

When I check the preview tab, it's a fancy preview mode, with all the nodes folded:

```
v [{id: 43,…}, {id: 44,…}, {id: 46,…}, {id: 45,…}]
> 0: {id: 43,…}
> 1: {id: 44,…}
> 2: {id: 46,…}
> 3: {id: 45,…}
```

Not easy to check the shape of the data either.

Solution
===

`JSON.stringify` to the rescue!


```js
function prettifyJson(json) {
  console.log(JSON.stringify(
    json,      // copied from Response tab
    undefined, // ignore this argument (or read link below)
    2          // spaces to indent
  ));
};
```

Paste the above into the Chrome inspector.

Then copy the response in the response tab, and call the function:

```
>> prettifyJson([{"id":43,"child_node":{"active":true,"name":"name","created_at":"2015-05-25T16:55:09.600-04:00"},"notes":null}])
```

Output:

```
[
  {
    "id": 43,
    "child_node": {
      "active": true,
      "name": "name",
      "created_at": "2015-05-25T16:55:09.600-04:00"
    },
    "notes": null
  }
]

// Tada!!
```

Resource:

https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/JSON/stringify
