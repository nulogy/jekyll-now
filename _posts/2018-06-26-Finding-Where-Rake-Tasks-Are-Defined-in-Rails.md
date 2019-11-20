---
layout: post
title: "Finding Where Rake Tasks Are Defined in Rails"
author: jasonschweier
date: 2018-06-26T16:32:39+00:00
---

Rake has an option to print where a task was loaded from.

```
$ rake -W gettext:find
rake gettext:find   $HOME/.rvm/gems/ruby-2.3.3/gems/gettext_i18n_rails-1.8.0/lib/gettext_i18n_rails/tasks.rb:64:in `block in <top (required)>'
```

We can also get this data with code. This allows us to explore the tasks (e.g. filtering). In a Rails console:

```ruby
# load up all the tasks Rails knows about
> Rails.application.load_tasks
...

# if you know the task you are looking for:
> Rake::Task["gettext:find"].actions.map(&:source_location)
 => [["$HOME/.rvm/gems/ruby-2.3.3/gems/gettext_i18n_rails-1.8.0/lib/gettext_i18n_rails/tasks.rb", 64]]
 
 # if you want to explore known tasks
 > gettext_tasks = Rake.application.tasks.select { |e| e.name.start_with? "gettext:" }
 => [<Rake::Task gettext:add_language => [environment]>, <Rake::Task gettext:base_without_table_attributes => [environment]>, <Rake::Task gettext:find => [setup]>, <Rake::Task gettext:pack => [setup]>, <Rake::Task gettext:setup => [environment]>, <Rake::Task gettext:store_model_attributes => [environment]>]
 >
 > pp Hash[gettext_tasks.map { |t| [t.name, t.locations] }]
 {"gettext:add_language"=>
  ["$HOME/.rvm/gems/ruby-2.3.3/gems/gettext_i18n_rails-1.8.0/lib/gettext_i18n_rails/tasks.rb:99:in `block in <top (required)>'"],
 "gettext:base_without_table_attributes"=>
  ["$HOME/src/packmanager/master/lib/tasks/gettext.rake:27:in `block in <top (required)>'"],
 "gettext:find"=>
  ["$HOME/.rvm/gems/ruby-2.3.3/gems/gettext_i18n_rails-1.8.0/lib/gettext_i18n_rails/tasks.rb:64:in `block in <top (required)>'"],
 "gettext:pack"=>
  ["$HOME/.rvm/gems/ruby-2.3.3/gems/gettext_i18n_rails-1.8.0/lib/gettext_i18n_rails/tasks.rb:59:in `block in <top (required)>'"],
 "gettext:setup"=>
  ["$HOME/.rvm/gems/ruby-2.3.3/gems/gettext_i18n_rails-1.8.0/lib/gettext_i18n_rails/tasks.rb:43:in `block in <top (required)>'"],
 "gettext:store_model_attributes"=>
  ["$HOME/.rvm/gems/ruby-2.3.3/gems/gettext_i18n_rails-1.8.0/lib/gettext_i18n_rails/tasks.rb:82:in `block in <top (required)>'"]}
```
