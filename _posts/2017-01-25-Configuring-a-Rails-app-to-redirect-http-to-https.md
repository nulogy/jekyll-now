---
layout: post
title: "Configuring a Rails app to redirect http to https"
author: clemenspark
date: 2017-01-25T16:18:57+00:00
---

Problem
===

I have a Rails app on Heroku that is serving up a site on http and https.
Google oAuth's callback URL is for https, so attempting to log into the site from the http URL fails.

Solution
===

The intention was to serve up the site just from the https url, so the solution is to configure Rails to redirect all http traffic to https.

In `config/production.rb`:

```ruby
  config.force_ssl = true
```

Resource: http://stackoverflow.com/questions/27377386/force-ssl-for-heroku-apps-running-in-eu-region
