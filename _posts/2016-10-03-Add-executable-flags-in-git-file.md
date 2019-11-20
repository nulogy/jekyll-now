---
layout: post
title: "Add executable flags in git file"
author: evanbrodie
date: 2016-10-03T16:02:53+00:00
---

There is support in the `git add` command to make a file tracked in your git repository executable. For example, let's say you added a `foo.sh` script to your repo but forgot to add the executable bit to its file permissions. You can now do this:

```sh
git add --chmod=+x foo.sh
```

One gotcha of this approach is that this will only change the permissions tracked by git, but not the actual permissions of the file on YOUR filesystem. You will still need to run `chmod +x foo.sh` to modify your local permissions. However, your teammates should be able to pick up the permission changes from a `git pull`.

Courtesy of http://stackoverflow.com/a/38285435/814576
