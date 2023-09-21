## Automating API Testing with AWS Code Pipeline, AWS Code Build, and Postman
+ create a s3 bucket```aws s3 mb s3://<unique-bckt-name>```
+ upload the postman collection to s3 ```aws s3 cp PetStoreAPI.postman_collection.json s3://<REPLACE_ME_WITH_UNIQUE_BUCKET_NAME>/postman-env-files/PetStoreAPI.postman_collection.json```
+  Save the Postman environment file to S3 using the AWS CLI
```aws s3 cp PetStoreAPIEnvironment.postman_environment.json s3://automatedtest-bckt/postman-env-files/PetStoreAPIEnvironment.postman_environment.json```
+ Use the AWS CLI to deploy the AWS CloudFormation template as follows
```
aws cloudformation create-stack --stack-name petstore-api-pipeline \
--template-body file://./petstore-api-pipeline.yaml \
--parameters \
ParameterKey=BucketRoot,ParameterValue=<REPLACE_ME_WITH_UNIQUE_BUCKET_NAME> \
ParameterKey=GitHubBranch,ParameterValue=<REPLACE_ME_GITHUB_BRANCH> \
ParameterKey=GitHubRepositoryName,ParameterValue=<REPLACE_ME_GITHUB_REPO> \
ParameterKey=GitHubToken,ParameterValue=<REPLACE_ME_GITHUB_TOKEN> \
ParameterKey=GitHubUser,ParameterValue=<REPLACE_ME_GITHUB_USERNAME> \
--capabilities CAPABILITY_NAMED_IAM
```
 aws cloudformation create-stack --stack-name petstore-api-pipeline --template-body file://./petstore-api-pipeline.yaml --parameters ParameterKey=BucketRoot,ParameterValue=automatedtest-bckt ParameterKey=GitHubBranch,ParameterValue=Main ParameterKey=GitHubRepositoryName,ParameterValue=Automated-API-postman-aws ParameterKey=GitHubToken,ParameterValue=ghp ParameterKey=GitHubUser,ParameterValue=PHIDELIST --capabilities CAPABILITY_NAMED_IAM