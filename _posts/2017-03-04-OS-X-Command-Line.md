---
layout: post
title: "OS X Command Line"
author: alistairmckinnell
date: 2017-03-04T17:57:58+00:00
---

I love being able to use [Alfred](https://www.alfredapp.com/) as a kind of GUI command line...

..and I also like using the command line to get things done. I just discovered all sorts of new things that I can do from the command line from this GitHub [repo](https://github.com/herrbischoff/awesome-osx-command-line).

For example, to show Wi-Fi Connection History:

```
defaults read \
  /Library/Preferences/SystemConfiguration/com.apple.airport.preferences | \
  grep LastConnected -A 7
```
