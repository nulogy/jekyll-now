---
layout: post
title: "[GIT] Change capitalization of file"
author: evanbrodie
date: 2016-06-30T17:34:58+00:00
---

**HOW DO I CHANGE THE NAME OF A FILE UNDER GIT CONTROL WHERE NOTHING CHANGES EXCEPT THE CAPITALIZATION OF THE LETTERS?**

For example, let's say that you had a file called `myfile.js` and you wanted to rename it to `MyFile.js`. This change would not be recognized in `git status` and therefore cannot be committed because none of the characters actually changed. It appears that git treats files in a ignores-case way when scanning for changes. Whereas, if I added or removed any of the characters in that name, ie `MyFile1.js`, then git would recognize the *rename*.

**SOLUTION**

[As per this Stackoverflow post](http://stackoverflow.com/questions/10523849/changing-capitalization-of-filenames-in-git), you can still commit this filename capitalization change using a `git mv` command. So in this example, we would want to execute this:

```
git mv myfile.js MyFile.js
```
