---
layout: post
title: "Bulk Upsert through PostgreSQL 9.5+"
author: joneriksuero
date: 2017-05-11T13:29:48+00:00
---

*Warning:* This only works for PostgreSQL 9.5+
___

Given the following:

1. a **users** table:
    - id
    - name
    - created_at
    - updated_at

1. **users** table only has 1 user with values:
    - id: 1
    - name: Alejandro
    - created_at: '2010-10-10 10:00:00.000000'
    - updated_at: '2010-10-10 10:00:00.000000'

You can upsert using the following SQL query:

```sql
INSERT INTO
  users(id, name, created_at, updated_at)
VALUES
  (1, 'Alexander', NOW(), NOW()),
  (2, 'Belle', NOW(), NOW())
ON CONFLICT (id)
  DO UPDATE SET
    name=EXCLUDED.name,
    updated_at=NOW()
;
```
___
Results:

1. User(id=1) will be renamed from *Alejandro* to *Alexander*. The *updated_at* value will be set to current time.
1. User(id=2) will be inserted to *users* table with name = *Belle*, and both *created_at* and *updated_at* will be set to current time.


