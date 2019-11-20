---
layout: post
title: "Changing Your iterm2 Profile Programmatically"
author: alistairmckinnell
date: 2017-05-03T11:33:15+00:00
---

Change your iterm2 profile to *Production* with this command:

````sh
echo -e “\033]50;SetProfile=Production\a”
````

Create a function to make it easier to switch profiles:

````sh
function iterm_profile {
  if [[ -z $1 ]]; then
    profile="Default"
  else
    profile=$1
  fi

  echo -e "\033]50;SetProfile=$profile\a"
}
````

I use this feature to let me know I am working on the Rails migration.

[Source](https://medium.com/@adriennedomingus/changing-your-terminals-appearance-based-on-environment-variables-ad9b2d145b34)

