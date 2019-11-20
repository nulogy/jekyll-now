---
layout: post
title: "Turn AWS tags into a useful data structure with jq"
author: justinfitzsimmons
date: 2017-01-27T18:12:09+00:00
---

The JSON responses from the AWS API contain tags in a data structure like this:

```
"Tags": [
    {
        "Value": "consul-test-jf",
        "Key": "Name"
    },
    {
        "Value": "test-jf",
        "Key": "consul-group"
    },
    {
        "Value": "server",
        "Key": "consul-role"
    }
]
```

This structure is awkward to query with jq, but you can map it into a normal object like this:

`jq '<path to Tags> | map({"key": .Key, "value": .Value}) | from_entries'`

Which returns an object that looks like this:

```
{
  "consul-role": "server",
  "consul-group": "test-jf",
  "Name": "consul-test-jf"
}
```

