---
layout: post
title: "Re-run only failed tests through Rspec"
author: jordanneville
date: 2016-04-22T17:22:39+00:00
---

In cases where large refactoring is taking place and there are multiple tests across multiple files failing, there's an easy shortcut built into Rspec that allows you to re-run your specs but _**only**_ the ones that failed.
<br/>
<br/>
The command
---------------------
    rspec --only-failures
<br/>
<br/>
This allows for a tighter feedback loop to get failing tests green.
<br/>
<br/>
Setup
----------
This functionality doesn't come for free and some simple, but required, setup is necessary. Details about what's required can be [found here.] (https://relishapp.com/rspec/rspec-core/docs/command-line/only-failures)

The quick rundown is your Rspec configuration needs some extra flags set:

    RSpec.configure do |c|
      c.example_status_persistence_file_path = "failing_specs.txt" 
      c.run_all_when_everything_filtered = true
    end

This is required so Rspec will output any failing specs to a file and then read from it when `--only-failures` is specified.

Permanently using this, it's also a great idea to add it to your `.gitignore` file.
