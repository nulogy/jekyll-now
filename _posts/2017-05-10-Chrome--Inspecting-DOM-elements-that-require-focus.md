---
layout: post
title: "Chrome: Inspecting DOM elements that require focus"
author: bryanmacdiarmid
date: 2017-05-10T20:46:42+00:00
---

Using Chrome Dev Tools, I occasionally want to inspect an element that requires focus - for example, inspecting a selected date in a date selector.

## Problem
As soon as I click the dev tools window, the element loses focus and I can no longer inspect in with the desired state.  

## Undesirable solution
On occasion when I've run into this scenario, I've placed a breakpoint or `debugger` statement in the JavaScript function that would be called when focus is lost. The problem with this is that it takes time and I need to locate the appropriate place in code.

## Better solution
When in the desired state - for example, with the current date selected - pressing `F8` will pause JavaScript execution.  I can then inspect the DOM in the desired state. 




