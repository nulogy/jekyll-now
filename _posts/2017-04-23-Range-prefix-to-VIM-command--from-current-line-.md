---
layout: post
title: "Range prefix to VIM command (from current line)"
author: evanbrodie
date: 2017-04-23T16:18:42+00:00
---

When I want to execute a command in VIM over a range of lines (for example, search-replace with `:s`) starting from the current line, I could execute a command like so:

```
:.,.+10s/foo/bar/g
```

This reads as search-replace from the current line (`.`) until 10 lines after. While useful functionality, it does require quite a bit of typing to execute.

Thankfully, there is a neat little shortcut that can be used to reduce some of this type. Simply enter the number of lines that you want to change from the current line and VIM will fill in the rest in the command prompt.

For example, I need to type `11:` and VIM will insert `:.,.+10` into the command prompt. You can now finish off this command like needed. Do note that the line count includes the current line itself (think of this count as current line plus number of lines after).
