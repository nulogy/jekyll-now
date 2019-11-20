---
layout: post
title: "Expect to Receive and Call to Original"
author: shahriyarnasir
date: 2016-04-08T20:18:19+00:00
---

In integration specs, it is preferable to call the original method when setting up an expectation on an object to receive an invocation of that method. This way, the method isn't stubbed out but instead will still be invoked. Any *downstream effects* of calling that method won't be hidden.

```ruby
class Calculator
  def self.add(x, y)
    x + y
  end
end
```

Should be tested like this:

```ruby
require 'calculator'

RSpec.describe "and_call_original" do
  it "responds as it normally would" do
    expect(Calculator).to receive(:add).and_call_original
    expect(Calculator.add(2, 3)).to eq(5)  # any bugs inside of #add won't be hidden
  end
end
```

This code example is taken from: [Relish - Calling the original implementation](https://relishapp.com/rspec/rspec-mocks/v/3-4/docs/configuring-responses/calling-the-original-implementation)
