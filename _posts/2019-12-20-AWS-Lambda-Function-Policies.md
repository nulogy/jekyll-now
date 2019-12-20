---
layout: post
title: "Using AWS Lambdas and API Gateway together: Function Policies"
author: podrezo
date: 2019-12-20
excerpt: "If you want to use a custom route for your lambda, and not just the generated route given by adding your lambda to your gateway automatically, you'll need to specifically enable a \"function policy\" to do so. The current function policy can be viewed by going to the lambda in the AWS console, going to \"permissions\" and scrolling down to the \"function policy\" section. This provides a read only, JSON-formatted view of the function policy for the lambda you're looking at. This view is read-only: It is not possible to manipulate the function policy from the AWS console and modifying it will require the use of either the AWS API or the [AWS CLI](https://aws.amazon.com/cli/). For the purposes of this post, we'll use the CLI. [Continued...]"
---

If you want to use a custom route for your lambda, and not just the generated route given by adding your lambda to your gateway automatically, you'll need to specifically enable a "function policy" to do so. The current function policy can be viewed by going to the lambda in the AWS console, going to "permissions" and scrolling down to the "function policy" section. This provides a read only, JSON-formatted view of the function policy for the lambda you're looking at. This view is read-only: It is not possible to manipulate the function policy from the AWS console and modifying it will require the use of either the AWS API or the [AWS CLI](https://aws.amazon.com/cli/). For the purposes of this post, we'll use the CLI.

Note the ARN of the lambda in the top right; for example `arn:aws:lambda:us-east-1:XXXXXXXXXX:function:MyFunction`. From here on in, I'll simply use the shorthand `$ARN` instead of the actual value. You can fetch the policy like so:

```bash
aws lambda get-policy --function-name $ARN
# {
#   "Version": "2012-10-17",
#   "Id": "default",
#   "Statement": [
#     {
#       "Sid": "lambda-xxxxxx",
#       "Effect": "Allow",
#       "Principal": {
#         "Service": "apigateway.amazonaws.com"
#       },
#       "Action": "lambda:InvokeFunction",
#       "Resource": "arn:aws:lambda:us-east-1:XXXXXXXXXX:function:MyFunction",
#       "Condition": {
#         "ArnLike": {
#           "AWS:SourceArn": "arn:aws:execute-api:us-east-1:xxxxxxxxxx:xxxxxxx/*/*/MyFunction"
#         }
#       }
#     }
#   ]
# }
```

This should return the same JSON document you can view from the console. Note the `Sid` values - you can reference a specific `Sid` to remove a policy from the function, such as the automatically generated policy that allows execution of the lambda on it's default route.

```bash
aws lambda remove-permission \
  --function-name $ARN \
  --statement-id lambda-xxxxxx
```

You can also add permissions for a new route. The statement ID can be any value you want, my recommendation is to just generate a UUID and use that:

```bash
aws lambda add-permission \
  --statement-id xxxxxxxxxx-xxxxxxxx-xxxxxx-xxxxx \
  --action lambda:InvokeFunction \
  --function-name $ARN \
  --principal apigateway.amazonaws.com \
  --source-arn "arn:aws:execute-api:us-east-1:xxxxx:xxxxxx/*/*/my/url/from/gateway"
```
