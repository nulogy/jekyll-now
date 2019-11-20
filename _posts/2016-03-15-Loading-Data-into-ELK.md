---
layout: post
title: "Loading Data into ELK"
author: adamkerr
date: 2016-03-15T02:08:41+00:00
---

## Scenario
I want to load data in to Elasticsearch

## Solution
Modify this script.

```ruby
require "elasticsearch"
require "typhoeus"
require "typhoeus/adapters/faraday"

client = Elasticsearch::Client.new(host: "localhost:9200")

scope = BackgroundTask
  .where("created_at > '2015-01-01'")
  .where("created_at < '2016-01-01'")

count_so_far = 0

puts "Processing #{scope.count} records"

scope
  .find_in_batches do |tasks|

  puts "#{count_so_far} of #{scope.count}"
  count_so_far += tasks.count

  task_array = tasks.map do |task|
    {
      create: {
        _index: "background_tasks",
        _id: task.id,
        _type: "task",
        data: {
          task_type: task.type,
          created_at: task.created_at,
          waiting_time: task.queued_at - task.created_at,
          queued_time: task.run_at - task.queued_at,
          processing_time: task.completed_at - task.run_at
        },
      }
    }
  end

  client.bulk(body: task_array)
end
```
