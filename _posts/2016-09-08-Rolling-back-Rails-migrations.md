---
layout: post
title: "Rolling back Rails migrations"
author: clemenspark
date: 2016-09-08T16:33:43+00:00
---

There are a bunch of ways to roll back migrations, so I figured I'd capture them in Q & A format.

Let's say the following migration files exist:

```
> ls db/migrate

20160613172644_migration_1
20160614173819_migration_2
20160615142814_migration_3
20160615160123_migration_4
20160615174549_migration_5
```

Q: How do I roll back the last migration.  
A: `rake db:rollback`

Q: How do I roll back the last 3 migrations?  
A: `rake db:rollback STEP=3`

Q: How do I roll back a specific migration?  
A: `rake db:migrate:down VERSION=20160615142814`  
Details:  
The timestamp comes from the filename: `20160615142814_migration_3`

and... the one I learned today:

Q: How do I roll back all the migration past a certain version?  
A: `rake db:migrate VERSION=20160615142814`.  
Details:  
The above will keep the following:

```
20160613172644_migration_1
20160614173819_migration_2
20160615142814_migration_3
```

and roll back the following:

```
20160615160123_migration_4
20160615174549_migration_5
```

In other words, it will keep all the migrations upto and including the version you specified.
