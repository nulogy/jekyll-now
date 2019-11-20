---
layout: post
title: "A quick deep dive into 'rake gettext:find'"
author: clemenspark
date: 2016-10-28T19:45:50+00:00
---

## Problem

I am using [Ruby Gettext](https://github.com/ruby-gettext/gettext) to manage
translations. But today, when I ran `rake gettext:find` to update my
[PO files](https://www.gnu.org/software/gettext/manual/html_node/PO-Files.html), none of them got updated.

Why??

## The Investigation

After some digging, I noticed that Ruby Gettext defines one
[FileTask](https://github.com/ruby/rake/blob/v11/lib/rake/file_task.rb) (a specific type of [Rake](https://github.com/ruby/rake) task) per
PO file, which delegates the work to [GNU
gettext](https://www.gnu.org/software/gettext/).

FileTask looks at the timestamps of dependent files, and
only executes the supplied block if any of the dependent files have a
timestamp later than the file to update.

For example:

```ruby
dependent_files = ["translations_template_file.pot"]
file "file_to_update" => dependent_files do
  # update the file
end
```

## Why `gettext:find` was not doing anything

It turned out that gettext uses two FileTasks.

One to update the template:

```ruby
files_needing_translations = ["file1.js", "file2.rb"]
file "translations_template_file.pot" => files_needing_translations do
  # update the translations template file
end
```

and another to update the PO file:

```ruby
file "en-US/translation_file.po" => ["translations_template_file.pot"] do
  # update "en-US/translations.po"
end
```

The reason `gettext:find` did not do anything was because none of the
files needing translation were updated, thus no PO files were updated.

## Solution

```
> touch one_of_the_files_that_gettext_looks_at.js
> rake gettext:find
```

