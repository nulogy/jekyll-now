---
layout: post
title: "React will conditionally batch calls to setState()"
author: jordanneville
date: 2016-12-07T19:56:29+00:00
---

React tries to be smart and batch calls to setState() when its being called from a UI event context (e.g. button click). This has ramifications on code as your setState() call is no longer synchronous and accessing `this.state` will actually refer to the old state.

E.g.

```
this.state = { hello: false };
...
onClick() {
   this.setState({ hello: true });
   console.log(this.state.hello); //<=== will print false instead of true
}
```

However, if the setState is in a context *not* from a UI event, setState becomes synchronous


```
this.state = { hello: false };
...
changeState() {
   this.setState({ hello: true });
   console.log(this.state.hello); //<=== will print true!
}
```

There's more info here on the topic of batching setState calls:
https://www.bennadel.com/blog/2893-setstate-state-mutation-operation-may-be-synchronous-in-reactjs.htm
