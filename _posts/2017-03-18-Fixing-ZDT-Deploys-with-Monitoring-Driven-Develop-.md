---
layout: post
title: "Fixing ZDT Deploys with Monitoring-Driven Develop."
author: arturopie
date: 2017-03-18T23:29:25+00:00
---

We were debugging a bug in our zero downtime deploy script. We tested the deploy using Chef, Kitchen and Vagrant. The bug was causing an error page to show for less than 3 seconds at the very end of the deploy. 

We used Monitoring Driven Development to consistently reproduce the bug (the red phase), and to validate our fix (the green phase). Here were the steps:

Preparation: 

1. `kitchen login # ssh to the vagrant box`
1. `sudo tail -fn100 /var/log/nginx/go.access.log    # to see the response codes from the server. If all responses show 200 code during the deploy, the deploy is working.`
1. Open other terminal window
1. `kitchen login   #  ssh to the vagrant box`
1. `watch -n 1 "curl localhost"   # make a request every 1 second`

Then we followed this feedback loop

On the host computer:

1. Make changes to the deploy recipe 
1. `kitchen converge   # this will run our deploy`
1. Check the output of the logs to see the result of the changes
1. Repeat the loop until bug is fixed

