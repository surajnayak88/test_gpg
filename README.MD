As a part of test we had to deploy an api using serverless offering from AWS (aws api gateway)
Which should basically render the output when we curl the newly deployed API

Steps followed:
1. First we created a new s3 bucket, in order to ensure the bucket name will be unique 
   always, we make use of random_pet resource, which appends random pets name and ensures
    buckets names are always unique.
2. Once ,the bucket is created, we have to create a lambda function. And in order to create and upload 
    lambda function archive we have to package the source code. we use archive_file data source 
    to generate a zip archive and upload it to the s3 bucket.
3. Now we create aws_lambda_function.hello_world set the runtime to nodejs 12.x
4. Create a cloud watch log group and iam role to access resources in aws account and finally
    attach the policy
5. Now, we create an HTTP API with API Gateway. we define the name as aws_apigatewayv2_api.lambda 
    and assign HTTP as the protocol
6. with the help aws_apigatewayv2_stage.lambda  define a stage 
7. Lastly, aws_apigatewayv2_route.hello_world  maps api gateway to our lambda function and create
   iam role to allow api gateway to invoke our lambda function. Along with a cloudwatch group to store 
   access logs 
