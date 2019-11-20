---
layout: post
title: "Add a role to all EC2 servers on a Chef Server"
author: ianpenney
date: 2016-03-09T17:42:52+00:00
---

```
knife exec -E 'nodes.find("ec2:*") { |n|
  n.run_list << "role[awsrole]" unless
  n.run_list.include?("role[awsrole]"); n.save }'
```

