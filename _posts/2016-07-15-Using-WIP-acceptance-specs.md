---
layout: post
title: "Using WIP acceptance specs"
author: clemenspark
date: 2016-07-15T14:29:35+00:00
---

Context
---

I usually follow the following approaching when working on a story:

1. Write a failing acceptance spec.
2. Do a spike to validate the proposed solution.  Get the spike to pass.
3. Capture learnings, and blow away the spike changes.
4. Properly TDD away at the solution.

One annoyance with this approach was:

What do I do with the failing acceptance spec?

I usually try not to commit failing specs, since that makes `git bisect` less useful when I'm trying to see what broke it.

Solution
---

RSpec tags to the rescue.

Configure your specs to ignore wip specs by default:

```ruby
RSpec.configure do |c|
  c.filter_run_excluding wip: true
end
```

Write a WIP spec:

```ruby
it 'tests my yet-to-be-added feature', :wip do
  "my test"
end
```

Run the spec:

```bash
rspec my_acceptance_spec.rb --tag=wip
```

The acceptance spec can be committed, because it won't run as part of your regular test suite.

Once the story is done, make sure you remove the :wip flag!
