`mkdir ~/.nvm
`
* open ~/.zshrc file and add following
`export NVM_DIR="$HOME/.nvm"
  [ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"  # This loads nvm
  [ -s "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm" ] && \. "/opt/homebrew/opt/nvm/etc/bash_completion.d/nvm"  # This loads nvm bash_completion
`

* set defualt node version to v16

`nvm alias default 16`

* upgrade stable version of node

`nvm install stable`

* list all the version
`nvm ls`
