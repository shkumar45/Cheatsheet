manually deploye lambda
- zip the file where handler function exists (typically called index.js), package.json, package-lock.json, node-modules folder and any other files reference in the handler file.
- copy the zip to s3
- create lambda function from aws console and use the zip file uploaded
- make sure a new role is created (sometimes orgs will only allow new role creation if boundary permissions are added)
  - Add AWSLambdaBasicExecutionRole if you you want cloudwatch logs are logged
- change runtime settings - Handler 
  - index.handler if the main file is index.js or app.handler in the main file is app.js
- quick testing can be done by making changes to the code->edit and deploy
- test lambda only from aws cli - aws lambda invoke --function-name <my-function>
