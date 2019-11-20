---
layout: post
title: "Use PostgreSQL table as queue skipping locked rows"
author: diogobiazus
date: 2017-03-22T22:00:24+00:00
---

This command **only works in PG 9.5**

First, are you sure you shouldn't be using some in-memory queue? Or some message broker? Or Redis?

If you are really convinced that you want this sort of behaviour on top of the goo'old PostgreSQL you can achieve a queue-like access pattern by locking and skipping locked rows.

One way to ensure that only one database client can modify a set of rows is to select the rows for update as in

    BEGIN;
    SELECT * FROM queue ORDER BY priority DESC LIMIT 1 FOR UPDATE;
    ...

This will block any other **UPDATE** or **SELECT .. FOR UPDATE** until the above transaction is finished.
Now if you want concurrent database clients to fetch the next row available in the priority list just use:

    BEGIN;
    SELECT * FROM queue ORDER BY priority DESC LIMIT 1 FOR UPDATE SKIP LOCKED;
    ...

The above command could be interpreted as "select the next row from queue that nobody has yet locked".
