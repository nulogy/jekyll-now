---
layout: post
title: "ZDT Column Rename in a Distributed System"
author: adamkerr
date: 2016-10-31T22:31:49+00:00
---

In order to deploy code to a highly available distributed system any two sequential versions of the code can be running at the same time. Therefore they need to be compatible.

1. Add the new column, keep the columns in sync when updating.
2. Migrate the data, start using the new column however fallback to the old column if the new column is blank, continue keeping the columns in sync.
3. Remove all dependencies on the old column, only use the new column, do not sync them anymore.
4. Drop the column.

When in Rails, Step #3 requires some special care as the column needs to be marked for removal:

```ruby
module MarkColumnsForRemoval
  def mark_columns_for_removal(*columns_marked_for_removal)
    @columns_marked_for_removal = columns_marked_for_removal.map(&:to_s)
  end

  ##
  # Overrides ActiveRecord's list of the database columns in order to hide a column which we intend to delete
  # This ensures that ActiveRecord does not try to read or write to the column
  #
  def columns
    cols = super
    cols.reject { |col| (@columns_marked_for_removal || []).include?(col.name.to_s) }
  end
end

class SomeModel < ActiveRecord::Base
  # Remove this as part of step 4 when dropping the old_column
  extend MarkColumnsForRemoval
  mark_columns_for_removal :old_column
end
````


