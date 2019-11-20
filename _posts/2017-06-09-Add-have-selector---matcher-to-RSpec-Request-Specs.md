---
layout: post
title: "Add have_selector() matcher to RSpec Request Specs"
author: jordanneville
date: 2017-06-09T18:38:18+00:00
---

If you are used to writing controller specs, you are probably comfortable with the `have_selector  matcher. However, in request specs this matcher is not available. By default, you can only do text search inside the request body which leads to brittle assertions.

You can add the `have_selector` matcher by updating your RSpec config to include the Capybara matchers on request specs as well.

`RSpec.configure do |config|`

`config.include Capybara::RSpecMatchers, type: :request`

`end`

Then you can write more confident Request specs by using assertions like `expect(response.body).to have_selector('ul li', text: 'List content here!')`
