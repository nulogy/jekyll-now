---
layout: post
title: "Diff CSVs With Ease"
author: jasonschweier
date: 2017-04-27T20:11:15+00:00
---

We're all familiar with diff tools like RubyMine, vimdiff, or the good old `diff` command. These work well for source code but are not optimal for CSVs files, which may have many columns and rows.

I found myself wanting to write CSV-specific diff tool, but I fought that *Not Invented Here* impulse and Googled first. I found a good Python library called [`csvdiff`](https://pypi.python.org/pypi/csvdiff).

Imagine we have the following CSV file:

```csv
id,name
1,Alan Turing
2,John McCarthy
3,Edger Djikstra
```

We want to compare it to another file:

```csv
id,name
1,Alan Turing
3,Edsger Dijkstra
4,John Von Neumann
```

We've removed, edited, and added a row. The summary option confirms our changes:

```sh
$ csvdiff --style=summary id one.csv two.csv
1 rows removed (33.3%)
1 rows added (33.3%)
1 rows changed (33.3%)
```

The detailed view gives us all the gory details:

```sh
$ csvdiff --style=pretty id one.csv two.csv
{
  "_index": [
    "id"
  ],
  "added": [
    {
      "id": "4",
      "name": "Jon Von Neumann"
    }
  ],
  "changed": [
    {
      "fields": {
        "name": {
          "from": "Edger Djikstra",
          "to": "Edsger Dijkstra"
        }
      },
      "key": [
        "3"
      ]
    }
  ],
  "removed": [
    {
      "id": "2",
      "name": "John McCarthy"
    }
  ]
}
```
