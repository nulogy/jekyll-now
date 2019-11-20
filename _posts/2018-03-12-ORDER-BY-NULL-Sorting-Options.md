---
layout: post
title: "ORDER BY NULL Sorting Options"
author: jasonschweier
date: 2018-03-12T17:03:13+00:00
---

The `ORDER BY` clause has options for placement of `NULL` columns. From the Postgres docs, the  [`ORDER BY` grammar](https://www.postgresql.org/docs/9.3/static/sql-select.html) is:

```
[ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
```

It shows we can put the `NULL` columns first or last.

## Example

Imagine we have a datetime range, implemented as (`start_at`, `end_at`) tuples.

```
CREATE TABLE dates (id INT, start_at TIMESTAMP, end_at TIMESTAMP);

INSERT INTO dates VALUES 
(1, TIMESTAMP '2018-01-01 9:45', TIMESTAMP '2018-01-01 10:00'),
(2, TIMESTAMP '2018-01-01 10:00', null),
(3, TIMESTAMP '2018-01-01 10:15', null);
```

We want to order by `end_at`, then `start_at`. However, we want the `NULL` `end_at` tuples to appear before any with a value.

By default, `NULL` values will appear *after* non-`NULL`. With the `NULLS FIRST` option, we can change that:

```
SELECT * FROM dates ORDER BY end_at NULLS FIRST, start_at, id;

╒══════╤═════════════════════╤═════════════════════╕
│ id   │ start_at            │ end_at              │
╞══════╪═════════════════════╪═════════════════════╡
│ 2    │ 2018-01-01 10:00:00 │ <null>              │
├──────┼─────────────────────┼─────────────────────┤
│ 3    │ 2018-01-01 10:15:00 │ <null>              │
├──────┼─────────────────────┼─────────────────────┤
│ 1    │ 2018-01-01 09:45:00 │ 2018-01-01 10:00:00 │
╘══════╧═════════════════════╧═════════════════════╛
```

You can also specify `NULLS` when [creating indexes too](https://www.postgresql.org/docs/9.3/static/indexes-ordering.html).
