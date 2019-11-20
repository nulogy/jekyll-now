---
layout: post
title: "Record File Handle Usage in OSX"
author: adamkerr
date: 2017-03-03T01:44:04+00:00
---

`lsof` is a helpful tool for looking at what files a process currently has open, however sometimes a process may only access a file for a second and `lsof` may miss the moment.

For OSX we also have **Instruments**. This is included with XCode and is pretty straight forward to use:

- Open Instruments
- Select *File Activity*
- Select the process
- Hit Record
- Perform your action
- Stop Recording

You can also save the log for later analysis.

