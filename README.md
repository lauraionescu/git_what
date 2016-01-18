# Advanced git concepts

The not-so-every day workflow

### Merging
#### Scenario 1: You need to add a new category of films, but that is not due to be released yet. Your team has decided that the work is going to be done on a branch, until the feature is ready to be released

Checkout a new brach called scifi  
Create a folder called scifi inside the movies folder  
Create a file blade_runner.txt in the scifi folder, using your favourite text editor  
Make changes to the file and commit them  
Push the branch to the remote repository  

```console
  git checkout -b scifi
  git add .
  git commit -m "Add Blade Runner to scifi films"
  git push -u origin scifi:scifi
  git log --pretty=oneline --decorate
```

#### The feature is nearly done, but there is some urgent work that needs to be done on master and you need to push a hotfix

Checkout master  
Add movies/film_noir/the_maltese_falcon.txt  
Push the change to master  

```console
  git checkout master
  git add .
  git pull
  git push
  git log --pretty=oneline --decorate
```

#### Let's finish the feature and merge it back to master

checkout the scifi branch  
Make a change in the blade_runner.txt file and push it to the remote  

```console
  git checkout scifi
  git add .
  git commit -m <Short meaningful message>
  git push
```

#### Merging

```console
  git checkout master
  git merge scifi
  git log --pretty=oneline
  git push
```

### Rebasing
#### Scenario 2: You are doing some experimental work locally, that is not yet ready to be pushed. You are working on a branch, in order to semantically differentiate it from the master

Create a branch called thriller  
Add thriller/spectre.txt to the branch  
**Don't push the changes yet!**

```console
  git checkout -b thriller
  git add .
  git commit -m "Add Spectre to thriller films"
  git log --pretty=oneline --decorate
```

#### The experimental work is nearly done, but there is some urgent work that needs to be done on master and you need to push a hotfix

Checkout master  
Make a change to film_noir/maltese_falcon.txt  
Push to the remote  

```console
  git checkout master
  git add .
  git pull
  git push
  git log --pretty=oneline --decorate
```

#### Let's finish the experimental work and merge it back to master

Edit the spectre.txt file and make another change

```console
  git checkout thriller  
  <edit spectre.txt>
  git add .
  git commit -m "Message"
  git rebase master
  git log --pretty=oneline --decorate --all --graph
  git checkout master
  git merge thriller
  git log --pretty=oneline --decorate --all --graph
```

### Interactive rebase
#### Scenario 3: You want to open source your movie data, but your commit history contains a lot information that should not be available to the wide world, so we need to clean all that up before releasing it

Create a branch called open-sourcing  
Create a directory called animation inside movies  
Add, commit movies/animation/my_neighbour_totoro.txt  
Add, commit movies/animation/the_cat_returns.txt  
Add, commit movies/animation/princess_mononoke.txt && animation/kikis_delivery_service.txt  
Make a change to movies/animation/the_cat_returns and commit  

**Don't push the changes to the remote yet**

Run interactive rebasing (before the commits have been pushed)  

```console
  git rebase -i HEAD~4
```

This will open up a text editor with the latest 4 commits  

Edit one of the commits (to split it in two)  

```console
  git reset HEAD~1
  git add movies/animation/princess_mononoke.txt
  git commit -m "Add Princess Mononoke"
  git add movies/animation/kikis_delivery_service.txt
  git commit -m "Add Kiki's delivery service"
  git rebase --continue
```
Reorder commits  
Squash commits  


### Conflicting changes
#### Scenario 4: You are making some important changes to the Scifi section that are not yet ready to be released. At the same time, you need to maintain the Scifi code that is already on master (conflicting changes)

Checkout the scifi branch  
This branch is behind master, as some work has been done on master since the last time we merged the branch  
Merge the master into the scifi branch  
Make some changes to the movies/scifi/blade_runner.txt file  
Commit and push those changes  

```console
  git checkout scifi
  git merge master
  git status
  git push
  <make some changes to blade_runner.txt>
  git add .
  git commit -m "Message"
  git push
```

Checkout master  
Make some other changes to the movies/scifi/blade_runner.txt file  
Commit the changes, but don't push them yet!  

```console
  git checkout master
  <make some other changes to blade_runner.txt>
  git add .
  git commit -m "Message"
```

#### Rebase the brach onto master, to make it ready for merging it back to master, while keeping the history clean

```console
  git checkout scifi
  git merge master
```

#### We now have to resolve the conflicts

Choose the version on the branch, using your favourite text editor  

``` console
  git add .
  git rebase --continue
```

#### The branch is now ready to be merged back to master

``` console
  git checkout master
  git merge scifi
```

### Other useful commands

git cherry-pick  
git reflog
  git updates reflog every time HEAD moves (can resurrect branches and lost work)    

### Useful resources

http://git-scm.com/book/  
https://www.atlassian.com/git/tutorials/  
