---
layout: post
title: "Using Trigram Indexes to Speed Up LIKE Queries"
author: jasonschweier
date: 2017-04-16T22:18:33+00:00
---

Queries containing `ILIKE '%anything%'` result in table scans since they have a leading wildcard. Typical `btree` indexes can not help improve performance in this case.

[Trigrams](https://www.postgresql.org/docs/9.5/static/pgtrgm.html) are 3-character slices of words:

```sql
SELECT show_trgm('Ruby');
-- {"  r"," ru","by ",rub,uby}
```

They are useful as indexes since they can speed up `LIKE`, `ILIKE`, `~`, and `~*` clauses.

Let's query a table of 14K email addresses:

```sql
CREATE TABLE emails (email TEXT);

\copy emails FROM 'emails.csv' DELIMITER ',' CSV;

EXPLAIN ANALYZE SELECT * FROM emails WHERE email ILIKE '%ion%';
```

The query plan shows a table scan:

```
Seq Scan on emails
  Filter: (email ~~* '%ion%'::text)
  Rows Removed by Filter: 14040
```

with an average execution time of `15ms`. Let's create a trigram index and try again:

```sql
-- postgres 9.2+
CREATE EXTENSION IF NOT EXISTS pg_trgm;

CREATE INDEX emails_search_email_idx ON emails USING GIN (email gin_trgm_ops);

EXPLAIN ANALYZE SELECT * FROM emails WHERE email ILIKE '%ion%';
```

The improved query plan is:

```
Bitmap Heap Scan on emails
  Recheck Cond: (email ~~* '%ion%'::text)
  Heap Blocks: exact=98
    -> Bitmap Index Scan on emails_search_email_idx
       Index Cond: (email ~~* '%ion%'::text)
```

and averages `0.8ms`. A 19X improvement without updating any SQL queries! YMMV
