---
layout: post
title: "Rails console options to make your life better"
author: ryanmagowan
date: 2016-04-20T20:37:38+00:00
---

Often when learning or testing out an implementation in planning, entering into a REPL to get some feedback and play with something more physical is desirable.

Here are some tips to improve your rails console workflow:

<h2>Specify the environment you wish to use</h2>

Maybe you want to try and reproduce an error in production during your test runs.  Maybe you want to seed the database for your development server before having created a seed file.  Maybe you're just feeling wild for the day and want to switch things up.

Rails gives you the option to select the environment for the console session:

```
>rails c --environment=test [test/development/production/...other...]
>rails c test  # as a shorthand
```
<i>Note: The default environment is set to development</i>

<h2>Sandbox so your DB entries do not persist</h3>

Often I find myself wanting to just play around with the current build, knowingly wanting to throw away the changes after.  Sandboxing is a great way to do this while reducing your cleanup workflow.

```
>rails c --sandbox
>rails c -s
```

This saves you from having to write out the following to return to a seeded state:

```
>rake db:reset RAILS_ENV=[environment]
```
