# Git Branch Model
# Github
## fork后与原仓库同步
```git
$ git remote add upstream {upstream github url}
---
$ git fetch upstream
$ git checkout master
$ git merge upstream master
---
$ git pull upstream master
```