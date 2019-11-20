---
layout: post
title: "Rails 4 Strong Parameters Gotcha: Array in Params"
author: paulsobocinski
date: 2016-04-12T20:34:19+00:00
---

When using strong parameters in Rails 4, any non-scalar parameters must be permitted using a special syntax. The following example is for when you are passing in an array of scalar values in a request parameter (and you are using Rails 4 Strong Parameters to whitelist the parameter).

Firstly, note that the following **will not work** (i.e. the spec will fail):

```ruby
# routes.rb
post '/thing/create' => 'thing#create'

# thing_controller_spec.rb
RSpec.describe ThingController, type: :controller do
  example do
    post :create, things: [1, 2, 3]

    expect(response.body).to eq('1,2,3')
  end
end

# thing_controller.rb
class ThingController < ApplicationController
  def create
    permitted_params = params.permit(:things)
    render inline: permitted_params[:things].join(',')
  end
end
```

Why does it fail? Rails is expecting a scalar value to be passed in the `:things` parameter. However, we pass in an array, so Rails silently removes the parameter, *even though it is included in the call to `params.permit`*.

In order to make the spec pass, we update the implementation as follows:

```ruby
# thing_controller.rb
class ThingController < ApplicationController
  def create
    permitted_params = params.permit(things: [])
    render inline: permitted_params[:things].join(',')
  end
end
```

For more info about strong parameters, especially in regards to how to permit non-scalar and nested parameters, please refer to: https://github.com/rails/strong_parameters#permitted-scalar-values.
