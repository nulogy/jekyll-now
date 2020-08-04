---
layout: post
title: "Ruby code with gems on AWS Lambda"
author: podrezo
date: 2019-12-20
excerpt: "If you want to use ruby with AWS's lambdas and that ruby code relies on gems then you'll have to jump through a small hoop to get it running. This article explains how. [Continued...]"
---

If you want to use ruby with AWS's lambdas and that ruby code relies on gems then you'll have to jump through a small hoop to get it running. Firstly, create a `.bundle/config` file in your lambda code's root directory. The contents of this file should be as follows:

```
---
BUNDLE_PATH: "vendor/bundle"
```

This will tell bundler to install the gems inside the `vendor/bundle` directory in the root of your project rather than in your home directory as is default. This allows us to package the gems together with the code when uploading the package to Amazon. You may want to add the `vendor` directory to your `.gitignore` file.

Now, add/install the gem you want to use. For our example, let's use `rest-client`:

```
bundle init
bundle add rest-client
```

Let's create a handler file to make use of this gem called `main.rb` as follows:

```ruby
require 'rest-client'

def handler
  response = RestClient.get 'https://jsonplaceholder.typicode.com/todos/1'
  puts response.body
end
```

If you try to execute this lambda now you'll get an error as follows:

```
cannot load such file -- rest-client
```

This is because while we've told bundler where to install the gems to, we haven't told the ruby runtime where to find the gems when it is actually executing the code. To do this, we need to set an environment variable called `GEM_PATH` and set it to `/var/task/vendor/bundle/ruby/2.7.0` (all the lambda files are placed into `/var/task` so you need the path to the gems located inside your `vendor/bundle/RUBY_VERSION` directory). Replace `2.7.0` with whatever version of ruby you're using. If you run the code now, you should see a successful output. That's it!

**BONUS TIP 1:** If you're using multiple lambdas for the same project and they mostly require the same gems, I highly recommend building a [gem layer](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) that can be shared across all the lambdas. The process is more or less the same, but everything related to gems is put inside the layer (`vendor/bundle`, `Gemfile`, `Gemfile.lock`, etc.) instead of the lambda package itself. In this case, you'll need to update your `GEM_PATH` to point to `/opt/ruby/2.7.0`. See [AWS Lambda Layer Docs](https://docs.aws.amazon.com/lambda/latest/dg/configuration-layers.html) for more information.

**BONUS TIP 2:** I highly recommend using [Serverless Framework](https://www.serverless.com/) to manage all this as it makes it quite easy to keep track of everything and deploy it.

**BONUS TIP 3:** If you need gems that have native extensions, like [nokogiri](https://rubygems.org/gems/nokogiri) then you will need an even more involved process that includes building the gem on an AWS-lambda-like environment using docker. Basically everything above is the same, but instead of doing `bundle install` you'd do something like `docker run -it --rm -v $PROJECT_DIR/gem_layer:/var/task lambci/lambda:build-ruby2.7 bundle install --without=development`. For more info check out [lambci/lambda(https://hub.docker.com/r/lambci/lambda/).
