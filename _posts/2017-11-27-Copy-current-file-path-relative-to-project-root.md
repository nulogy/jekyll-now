---
layout: post
title: "Copy current file path relative to project root"
author: arturopie
date: 2017-11-27T22:41:14+00:00
---



I already knew about copying the current file path to the clipboard by using `Shift+Cmd+C` . The problem with this approach is that it copies the absolute path, for example, `/Users/arturo/src/cool_project/lib/module/my_file.rb`. This is not ideal if you are planning on sending this path to someone else or for some document you are writing. 

A better option is to use RubyMine's Action `Copy Reference` which by default is bound to `Shift+Alt+Cmd+C`. This copies the current file path relative to the project, for example, `lib/module/my_file.rb`

## To summarize:

**Copy Paths Action**

* Default shortcut: Shift+Cmd+C
* Example text to clipboard: `/Users/arturo/src/cool_project/lib/module/my_file.rb`

**Copy Reference  Action**

* Default shortcut: Shift+Alt+Cmd+C
* Example text to clipboard: `lib/module/my_file.rb`

Thanks to Jordan N. for the tip!
