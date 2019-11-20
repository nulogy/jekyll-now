---
layout: post
title: "Accessing Redux Store Without Redux DevTools"
author: evanbrodie
date: 2018-08-02T17:47:35+00:00
---

*Thank you [Dan Ambrogio](https://github.com/JackAnansi) for discovering this tip. Also, check out [this blog post](https://medium.com/@zalmoxis/using-redux-devtools-in-production-4c5b56c5600f) for more on the topic of Redux DevTools on production environments.*

Let's say that you want to access the Redux Store on a production environment of your React/Redux application. Normally, you would do this through the [Redux DevTools](https://github.com/zalmoxisus/redux-devtools-extension). However, your app has these DevTools disabled on production. What do you do then?

As long as your browser has the [React DevTools](https://github.com/facebook/react-devtools) installed, there's this awesome workaround (assuming you are using Chrome, could easily be ported to other browsers):

* Navigate to the web page in question
* Open up the Chrome DevTools
* Click on the React tab
* Click on the top-level `<Provider>` element/component
* Press `<ESC>` to bring up a console in a split panel
* Execute the following code: `$r.store.getState()`. VOILA!
