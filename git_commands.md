## using multiple ssh key
### make sure you set the user.email before making the very first commit on local. Else it is quite possible it picks up the github user from global config
### steps
```
git init
git config user.email "abc@mydomain.com"
git add *
git commit -u "my first commit"
git remote add git@github.com-personal:xyz/blank_new_repo.git
git push -u origin main 
```

## setup multipla ssh keys for multiple git accounts
### tbd

## It undoes the most recent commit whilst keeping the changes made in that commit to staging

``` git reset --soft HEAD~1 ```

