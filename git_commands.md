
## How to setup multiple ssh keys for multiple git accounts on one machine
follow the article

[Generating a new ssh key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key) 

[Adding your SSH key to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent)

## using multiple ssh key
Make sure **you set the user.email before making the very first commit on local**. Else it is quite possible it picks up the github user from global config
### steps
```
git init
git config user.email "abc@mydomain.com"
git add *
git commit -u "my first commit"
git remote add git@github.com-personal:xyz/blank_new_repo.git
git push -u origin main 
```

## It undoes the most recent commit whilst keeping the changes made in that commit to staging
``` git reset --soft HEAD~1 ```

