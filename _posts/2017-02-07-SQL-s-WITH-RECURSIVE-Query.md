---
layout: post
title: "SQL's WITH RECURSIVE Query"
author: jasonschweier
date: 2017-02-07T01:53:55+00:00
---

While optimizing calls to a recursive table, we found a neat SQL solution. It uses a [common table expression](https://en.wikipedia.org/wiki/Hierarchical_and_recursive_queries_in_SQL#Common_table_expression) as a working table to query against iteratively.

Here's an example of using `WITH RECURSIVE` with a modified [nested set example of clothing categories](https://en.wikipedia.org/wiki/Nested_set_model#Example) that find all paths through the categories:

```sql
CREATE TEMPORARY TABLE categories (id INT, name text, parent_category_id INT);

INSERT INTO categories VALUES
  (1, 'Clothing', null),
  (2, 'Mens''s', 1),
  (3, 'Women''s', 1),
  (4, 'Suits', 2),
  (5, 'Dresses', 3),
  (6, 'Skirts', 3),
  (7, 'Jackets', 4),
  (8, 'Evening Gowns', 5);
  
WITH RECURSIVE category_hierarchies AS
(SELECT id, parent_category_id, name AS full_path
 FROM categories
 WHERE parent_category_id is NULL

 UNION ALL

 SELECT child_categories.id,
        child_categories.parent_category_id,
        parent_categories.full_path || ' -> ' || child_categories.name as full_path
 FROM categories AS child_categories
 INNER JOIN category_hierarchies AS parent_categories
   ON child_categories.parent_category_id = parent_categories.id
)
SELECT full_path FROM category_hierarchies ORDER BY full_path;
```

Produces paths through all categories:

* Clothing
* Clothing -> Mens's
* Clothing -> Mens's -> Suits
* Clothing -> Mens's -> Suits -> Jackets
* Clothing -> Women's
* Clothing -> Women's -> Dresses
* Clothing -> Women's -> Dresses -> Evening Gowns
* Clothing -> Women's -> Skirts

Read more about [`WITH RECURSIVE` queries](https://www.postgresql.org/docs/current/static/queries-with.html)
