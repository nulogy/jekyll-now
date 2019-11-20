---
layout: post
title: "Fix Mac RubyMine Floating Window Bug"
author: evanbrodie
date: 2016-05-09T21:09:57+00:00
---

PROBLEM
=====

On RubyMine in Mac, I want to have my RubyMine IDE in one window but have the Run display in **Floating Mode** appear in my secondary monitor.  The issue, though, is that after I have moved the Run display into my secondary monitor, lose focus to another window, then click back into the Run display, the will suddenly JUMP to the same window as my main RubyMine IDE.

SOLUTION
=====

The problem appears to be a conflict with a setting in Mac's Mission Control. You will need to deselect the "Displays have separate spaces" option in the Mission Control preferences screen, as [described here](http://apple.stackexchange.com/questions/116557/how-to-make-each-display-a-separate-space-yet-have-a-keyboard-shortcut-to-move).

#thanksapple
