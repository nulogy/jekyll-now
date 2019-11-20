---
layout: post
title: "Usage of $0 in the Chrome dev tools"
author: fabricecastel
date: 2016-05-30T19:34:34+00:00
---

In the Chrome dev console, typing `$0` evaluates to the last selected HTML element (by clicking on it under the 'Elements' tab). `$1` is the second last selected, up to `$4` - and despite the `$` this works independently of jQuery.

https://developer.chrome.com/devtools/docs/commandline-api#0-4
