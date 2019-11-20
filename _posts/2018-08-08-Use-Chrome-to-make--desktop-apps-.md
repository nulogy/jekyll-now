---
layout: post
title: "Use Chrome to make \"desktop apps\""
author: jasonkurian
date: 2018-08-08T21:18:16+00:00
---

You can use Chrome to make slick desktop apps for your frequently used tabs, and even make aliases:

```sh
alias twitter="open -na 'Google Chrome' --args '--app=https://mobile.twitter.com'"

# replace #{UID} with the index of the google account you want to use
# if you are signed in to multiple accounts on your computer, otherwise 0 should be fine.
alias cal="open -na 'Google Chrome' --args '--app=https://calendar.google.com/calendar/b/#{UID}/r'"

# for fun
alias pm="open -na 'Google Chrome' --args '--app=https://packmanager.nulogy.net/'"
```

Original tweet: https://twitter.com/JaKXz92/status/1025050967111344128, credits to Elijah Manor!
