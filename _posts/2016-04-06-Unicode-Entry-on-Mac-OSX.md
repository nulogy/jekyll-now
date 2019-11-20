---
layout: post
title: "Unicode Entry on Mac OSX"
author: ryandevilla
date: 2016-04-06T20:59:43+00:00
---

If you have the code point of a Unicode character, it is possible to enter these characters into (almost) any program on Mac OSX, by first jumping through a few hoops:

* Open *Language & Region*.
* At the bottom right, open *Keyboard Preferences...*
* Click the plus sign at the bottom left to add a new Input Source.
* Under the *Others* category, select the *Unicode Hex Input* source.
* Check the *Show Input menu in menu bar* option.

You should now see a country flag in your menu bar, which will allow you to switch between different Input Sources (e.g. Canadian English, U.S, Unicode Hex Input). Whenever you want to enter Unicode characters, switch to the *Unicode Hex Input* source.

Now, you can hold down ⌥ (Option/Alt) and enter your code point to type Unicode characters. For instance, the ⌥ character has code point 2325 and can be entered by holding Option and entering "2325".
