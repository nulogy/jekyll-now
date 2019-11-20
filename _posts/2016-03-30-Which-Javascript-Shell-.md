---
layout: post
title: "Which Javascript Shell?"
author: cameronwoloshyn
date: 2016-03-30T22:50:17+00:00
---

When it comes to Javascript Shells, there's a [long list to choose from](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Shells), but typically, when I want to play with Javascript, the easiest way is to simply open up a console in Chrome.

Recently, I've switched over to using [SpiderMonkey's](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey) Javascript shell because it allows me to execute a JS file and then drop into the shell.

## Installation:
`$ brew install spidermonkey`

## Vanilla Use Case:

Open up a shell with `js` command:

```
$ js
js> var obj = {a: 1};
js> obj;
({a:1})
js>
```

## How to execute a file and then drop into the shell:

Given a file `example.js` with the following contents: 

```
var a = 42;
```

Execute the file (`-f`) and continue in interactive mode (`-i`):

```
$ js -f example.js -i
js> a;
42
```

Check out the [docs](https://developer.mozilla.org/en-US/docs/Mozilla/Projects/SpiderMonkey/Introduction_to_the_JavaScript_shell) for a full list of options.
