prerequisite
aws cli
docker
aws sam cli
vscode - aws toolkit

commands
sam build
sam local start-api [--env-vars env.json] [-d 5858]


debugging tips
use the command pallet to create the debug configuration in .vscode/launch.js
  * type - aws-sam, request - direct_invoke (worked)
  * type - debugpy, request - attach (also working),  comment - trick is to invoke the api using postman so the debug port opens up then attach the debugger to the port.

