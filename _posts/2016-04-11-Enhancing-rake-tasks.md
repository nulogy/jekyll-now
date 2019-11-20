---
layout: post
title: "Enhancing rake tasks"
author: clemenspark
date: 2016-04-11T22:07:55+00:00
---

**Problem**

I have a rake task, and I want to make it do something before and after it's done.

```rb
task :a_task do
  puts "task"
end

task :setup_task do
  puts "setup"
end

task :run_after do
  puts "after"
end
```

What are my options?

**Solution**

For pre-req tasks, this is what is often done:

```rb
task :a_task => [:setup_task] do
  puts "task"
end

task :setup_task do
  puts "setup"
end
```

```
> rake a_task
setup
task
```

However, this requires modifying the existing task.  This might not even be an option for rake tasks from 3rd party gems.
We can do better: Enhance the task!

```rb
task :a_task do
  puts "task"
end

task :setup_task do
  puts "setup"
end

Rake::Task[:a_task].enhance [:setup_task]
```

```
> rake a_task
setup
task
```

To run a task (or any code for that matter) after a rake task:

```rb
task :a_task do
  puts "task"
end

task :run_after do
  puts "after"
end

Rake::Task["a_task"].enhance do
  Rake::Task["run_after"].invoke
end
```

```
> rake a_task
task
after
```

*Source: http://www.dan-manges.com/blog/modifying-rake-tasks*
