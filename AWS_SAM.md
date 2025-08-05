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
  type - direct_invoke (worked)
       - attach (not working)

