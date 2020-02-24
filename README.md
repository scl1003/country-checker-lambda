# country-checker-lambda

This is a sample python lambda to do sanction country blocking as a AWS API Gateway custom authorizer

# Steps to use

1. Find a service provider of ip address look-up. This example uses a free account from ipstack.com which gives 10000 free lookups per month.

2. Create a lambda from scratch with code in lambda\country-checker.py. Create a basic lambda role if needed (that just needs CloudWatch logs CreateLogGroup/CreateLogStream/PutLogEvents permission).

3. Go to API gateway / Authorizers, configure a custom authorizer according to https://aws.amazon.com/blogs/compute/using-enhanced-request-authorizers-in-amazon-api-gateway/ . The key is that this needs to use "Request" as the lambda event payload. Make sure you have configured a identity sources - e.g. Header.Authorization. With this setting, I used Postman's AWS authoirsation header method and configure with a set of access key / secret to test.

You should be able to see the looked up country code in the CloudWatch logs. You can change the lines in the python code that generate the policy document output that determines if the request is allowed or denied.


