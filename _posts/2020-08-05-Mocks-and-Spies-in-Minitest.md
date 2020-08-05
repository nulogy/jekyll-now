---
layout: post
title: "Mocks & Spies in Minitest"
author: podrezo
date: 2020-08-05
excerpt: "For one of our smaller ruby projects we didn't want to bring in all of rspec, so we decided to go with minitest as our unit test runner and assertion library. Doing mocks and spies in minitest proved a little bit challenging to get the hang of initially but it's actually quite easy. This article will explain how to do it."
---
For one of our smaller ruby projects we didn't want to bring in all of rspec, so we decided to go with minitest as our unit test runner and assertion library. Doing mocks and spies in minitest proved a little bit challenging to get the hang of initially but it's actually quite easy. This article will explain how to do it.

First, let's consider two classes - one helper class which we will be mocking out, and the other is the class under test.


```ruby
class MyHelperClass
  def upcase_instance(value)
    # value.upcase
    raise "Fail the test if the real thing is called"
  end

  def self.upcase_static(value)
    # value.upcase
    raise "Fail the test if the real thing is called"
  end
end

class MyClassUnderTest
  def use_upcase_instance(value)
    helper_class = MyHelperClass.new
    helper_class.upcase_instance(value)
  end

  def use_upcase_static(value)
    MyHelperClass.upcase_static(value)
  end
end
```

Note that if the real helper class's methods are called the test will fail to illustrate that we're doing the correct thing. In your test spec file you wil need to bring in the necessary `require`s for minitest:

```ruby
require "minitest/autorun"
require "minitest/mock"
```

The core aspect of mocking in minitest comes from `Minitest::Mock`'s `expect` method coupled with the `stub` method on whatever you're mocking. The [expect method signature](https://www.rubydoc.info/gems/minitest/Minitest/Mock) looks like this:

```ruby
expect(name, retval, args = [], &blk) ⇒ Object
# Expect that method name is called, optionally with args or a blk, and returns retval.
```

So we can mock out an instance method like so:

```ruby
mock = Minitest::Mock.new # Create a new mock
mock.expect(:upcase_instance, "FOURTYTWO", ["FoUrTyTwO"]) # Expect the upcase_instance method to be called with one argument "FoUrTyTwO" and force it to return the value "FOURTYTWO"
MyHelperClass.stub(:new, mock) do # Swap out the real implementation of the "new" method of MyHelperClass to return our mock
  MyClassUnderTest.new.use_upcase_instance("FoUrTyTwO") # Use the method. The expectation has already been set in the previous line
end
```

There is an additional library you can add called [bogdanvlviv/minitest-mock_expectations](https://github.com/bogdanvlviv/minitest-mock_expectations) which can make this a lot simpler if you find yourself writing a lot of mocks and spy assertions. With it we can rewrite the above as

```ruby
assert_called_on_instance_of(MyHelperClass, :upcase_instance, ["FoUrTyTwO"], returns: "FOURTYTWO") do
  MyClassUnderTest.new.use_upcase_instance("FoUrTyTwO")
end
```

And for a static method you write

```ruby
assert_called(MyHelperClass, :upcase_static, ["FoUrTyTwO"], returns: "FOURTYTWO") do
  MyClassUnderTest.new.use_upcase_static("FoUrTyTwO")
end
```

That's it!